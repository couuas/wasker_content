---
title: "OpenClaw 最佳实践调研报告"
date: 2026-03-01
category: "Tech"
description: "一份关于 OpenClaw 在多 Agent 协作、自动化工作流、Cron 任务及浏览器自动化等核心场景下的最佳实践汇总。"
tags: ["OpenClaw", "Best Practices", "Workflow", "Automation"]
---

# OpenClaw 最佳实践调研报告

## 1. 典型使用场景

### 1.1 多 Agent 协作配置 (Multi-Agent Collaboration)
OpenClaw 采用 C-Suite 架构模型，将不同职责分配给特定的 Agent。
- **God (CEO)**: 决策中心，负责任务分发和最终确认。
- **COO**: 负责执行、调度和协调。
- **CTO**: 技术架构、代码实现和风险评估。
- **CMO**: 市场、文案、调研和分发。

**最佳实践：**
- **模型混合策略**: 使用高智能模型（如 Claude 3.5 Sonnet）进行复杂推理，使用轻量模型（如 Gemini 1.5 Flash）处理简单任务或 Cron 任务，可降低 60-80% 的成本。
- **隔离与路由**: 在 `openclaw.json` 中定义 `agents.list`，并通过 `bindings` 将特定的频道或用户绑定到特定 Agent。

### 1.2 自动化工作流 (Automation Workflow)
通过 `sessions_spawn` 实现任务解耦，避免阻塞主会话。
- **Runner 模式**: 耗时较长的 `exec` 任务（如编译、大数据处理）应在独立的子 session 中运行。
- **注入模式 (Injection)**: 主 Agent 可以向专家 Agent 注入 session 以获取专业意见。

### 1.3 定时任务 (Cron Jobs)
OpenClaw 内置 Cron 服务，支持周期性任务和一次性任务（at）。
- **配置要点**: 任务需在 `cron` 字段中配置，且必须包含 `"enabled": true`。
- **时区处理**: 未指定时区时默认使用 UTC。
- **清理机制**: 一次性任务执行成功后默认删除，可通过 `deleteAfterRun: false` 保留并禁用。

### 1.4 浏览器自动化 (Browser Automation)
支持 Headless Chromium 截图和 UI 交互。
- **环境隔离**: 建议在沙箱模式下运行浏览器，配置 `sandbox: { mode: "non-main" }`。
- **兜底方案**: 当内置 `browser` 工具不可用时，可使用系统安装的 Chromium 命令行进行截图并拷贝回工作目录。

### 1.5 消息路由配置 (Message Routing)
通过 `bindings` 灵活控制消息流向。
- **匹配规则**: 支持按 `channel`、`teamId`、`peer.id`、`peer.kind` 匹配。
- **路由逻辑**: 私聊消息通常合并到 Agent 的 `main` session，群组或频道消息按 `channelId` 隔离。

---

## 2. 关键配置示例与代码片段

### 2.1 `openclaw.json` 基础结构
```json
{
  "agents": {
    "defaults": {
      "workspace": "~/.openclaw/workspace",
      "sandbox": { "mode": "non-main" }
    },
    "list": [
      { "id": "god", "model": "anthropic/claude-3-5-sonnet" },
      { "id": "cmo", "model": "google/gemini-1.5-flash" }
    ]
  },
  "bindings": [
    {
      "match": { "channel": "telegram", "peer": { "kind": "group", "id": "-100123456" } },
      "agentId": "cmo"
    }
  ],
  "cron": {
    "jobs": [
      {
        "id": "daily-report",
        "schedule": "0 9 * * *",
        "prompt": "生成昨天的日报并发送到管理员频道",
        "enabled": true
      }
    ]
  }
}
```

### 2.2 多模型分流 (TypeScript 代码逻辑示例)
```typescript
// 伪代码：在自定义 Skill 中根据任务复杂度选择模型
async function runTask(task: string) {
  const model = isComplex(task) ? "claude-3-5-sonnet" : "gemini-1.5-flash";
  return await subagents.spawn({
    agentId: "god",
    model: model,
    message: task
  });
}
```

---

## 3. 性能与限制优化
- **上下文管理**: `MEMORY.md` 和工作空间文件会占用 Context Window。建议保持文件精简，或使用 `memory_search` 进行检索。
- **失败恢复**: Cron 任务可能因提示词过长或上下文压缩而失败。建议在 Cron 任务中使用精简的 System Prompt。
- **安全防护**: 高风险操作（如 `rm`）应使用 `trash` 代替，或在 `openclaw.json` 中配置 `approval` 策略。
