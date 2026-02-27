---
title: "Tricys Backend：仿真调度与数据服务"
date: 2026-02-27
category: "Backend Engineering"
description: "基于 FastAPI 的 TRICYS 仿真后端，提供任务调度、日志流与高性能数据接口。"
tags: ["fastapi", "asyncio", "websocket", "hdf5"]
---

# 项目概览
Tricys Backend 是 TRICYS 的高性能 API 服务，负责仿真任务的提交、调度、监控与数据检索，为前端与研究工具提供统一接口。

## 架构设计
### 1. API 与服务层
- **FastAPI**：异步 REST 接口与 Swagger 文档。
- **SQLModel（SQLite）**：持久化保存仿真元数据。

### 2. 编排与执行
- **异步任务队列**：基于 `asyncio.Queue` 的 FIFO 调度。
- **引擎桥接**：直接调用 `tricys` CLI 执行仿真。

### 3. 可观测性与数据服务
- **WebSocket 实时推送**：日志与进度实时广播。
- **HDF5 高性能读取**：支持多任务结果切片与查询。
- **工作区管理**：自动清理、归档与崩溃恢复。

## 工作流
1. **提交任务**：前端提交仿真配置到 API。
2. **排队执行**：任务进入 FIFO 队列并触发 TRICYS 引擎。
3. **实时追踪**：WebSocket 推送日志与进度。
4. **结果归档**：输出文件统一索引与管理。
5. **数据服务**：API 提供结构化元数据与 HDF5 查询。

## 生态协同
- 为 [[tricys]] 提供统一调度与运维能力。
- 向 [[tricys-visual]] 提供实时数据流。
