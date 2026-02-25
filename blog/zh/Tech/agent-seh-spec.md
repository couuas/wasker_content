---
title: "代理侧效应哈希 (SEH)：技术规范"
date: 2026-02-25
category: "Tech"
description: "一种用于为代理工具调用产生的状态变化生成确定性、可验证哈希的协议。"
tags: ["AI 代理", "安全", "协议"]
---

# 草案：代理侧效应哈希 (SEH) - 技术规范

**状态**: Draft (草案)  
**版本**: 0.1.0  
**作者**: Agent God (@couuas)

## 1. 摘要 (Abstract)
随着 AI 代理从只读观察者转变为数字环境的主动操作者，对可验证的“侧效应归属”需求变得至关重要。代理侧效应哈希 (SEH) 是一种协议，用于为代理工具调用产生的状态变化（侧效应）生成确定性的、可验证的哈希值。

## 2. 动机 (Motivation)
- **不可抵赖性 (Non-Repudiation)**：证明特定的代理导致了特定的系统变更。
- **可审计性 (Auditability)**：为高后果操作创建防篡改日志。
- **共识机制 (Consensus)**：允许并行代理系统验证彼此工作的完整性。

## 3. SEH 算法 (The SEH Algorithm)
SEH 值是一个复合哈希：
`SEH = H(AgentID | SessionID | ToolName | InputArguments | PreStateDelta | PostStateDelta | Timestamp)`

### 3.1 状态增量 (State Deltas)
与完整的系统快照不同，SEH 专注于**最小增量**。
- **执行前增量 (PreStateDelta)**：操作前涉及资源的哈希。
- **执行后增量 (PostStateDelta)**：操作后涉及资源的哈希。

## 4. 实施模式 (Implementation Patterns)
- **中间件 (Middleware)**：在 OpenClaw 网关层拦截工具调用。
- **证明机制 (Attestation)**：使用代理私钥对 SEH 进行签名。

## 5. 使用场景 (Use Cases)
- **Git 提交归属**：在提交信息中包含 SEH 以验证 AI 生成的代码。
- **金融交易**：将代理主导的交易锚定到可验证的执行轨迹。
