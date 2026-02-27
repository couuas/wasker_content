---
title: "Tricys Visual：实时仿真可视化前端"
date: 2026-02-27
category: "Web Development"
description: "基于 Vue 3 的 TRICYS 前端，提供实时监控、三维可视化与 GoView 大屏集成。"
tags: ["vue", "threejs", "visualization", "dashboard"]
---

# 项目概览
Tricys Visual 是 TRICYS 生态的 Vue 3 前端，用于实时监控仿真任务、展示数字孪生与分析结果，使复杂数据以交互方式呈现。

## 架构设计
### 1. 特性分层结构
```
src/
├── api/         # API 客户端与服务模块
├── components/  # 通用、布局与特性组件
├── composables/ # 组合式 API Hooks
├── layouts/     # 页面布局
├── router/      # 路由配置
├── styles/      # 主题与全局样式
├── utils/       # 工具函数
└── views/       # 顶层页面
```

### 2. 可视化与交互层
- **Three.js 数字孪生**：交互式三维展示系统结构与组件关系。
- **结果分析工具**：内置 HDF5、Markdown 等文件浏览与可视化能力。

### 3. 实时数据与大屏集成
- **WebSocket 监控**：实时获取仿真 KPI 与任务进度。
- **GoView 嵌入**：低代码大屏仪表盘快速集成。

## 工作流
1. **本地启动**：安装 Node.js（v16+），执行 `npm install` 与 `npm run dev`。
2. **配置接口**：设置 `VITE_API_URL` 指向 Tricys Backend，`VITE_GOVIEW_URL` 指向大屏服务。
3. **运行监控**：实时查看任务进度与 3D 可视化效果。
4. **结果分析**：浏览仿真产出与报告文件。

## 生态协同
- 从 [[tricys-backend]] 获取任务与数据服务。
- 展示 [[tricys]] 生成的模型与报告结果。
