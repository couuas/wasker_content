---
title: "Tricys Backend: Simulation Orchestration API"
date: 2026-02-27
category: "Backend Engineering"
description: "FastAPI service for scheduling TRICYS simulations, streaming logs, and serving high-performance data APIs."
tags: ["fastapi", "asyncio", "websocket", "hdf5"]
---

# Project Overview
Tricys Backend is a high-performance RESTful API service that manages the full lifecycle of TRICYS simulations. It provides task scheduling, real-time observability, and data retrieval for large-scale simulation workloads.

## Architecture Design
### 1. API & Service Layer
- **FastAPI**: Async REST endpoints with OpenAPI/Swagger documentation.
- **SQLModel (SQLite)**: Persistent metadata for simulations and artifacts.

### 2. Orchestration & Execution
- **Async Task Queue**: FIFO scheduling using `asyncio.Queue`.
- **Engine Bridge**: Direct integration with the `tricys` CLI to execute simulations.

### 3. Observability & Data Services
- **WebSocket Streaming**: Live log and progress updates for active runs.
- **HDF5 Data Access**: High-performance slicing/querying for multi-job results.
- **Workspace Management**: Cleanup, archiving, and crash recovery for long-running tasks.

## Workflow
1. **Submit Simulation Task**: Frontend posts a job definition to the API.
2. **Queue & Execute**: Task enters the FIFO scheduler and invokes the TRICYS engine.
3. **Stream Updates**: Logs and progress pushed through WebSockets.
4. **Store Artifacts**: Outputs are indexed for fast retrieval.
5. **Serve Results**: Clients query structured metadata and HDF5 slices.

## Ecosystem Integration
- Provides the orchestration backbone for [[tricys]] simulations.
- Serves real-time data streams to [[tricys-visual]] dashboards.
