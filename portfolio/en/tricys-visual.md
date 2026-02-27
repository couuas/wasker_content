---
title: "Tricys Visual: Real-time Simulation Frontend"
date: 2026-02-27
category: "TRICYS"
description: "Vue 3 frontend for TRICYS with real-time monitoring, 3D visualization, and GoView dashboard integration."
tags: ["vue", "threejs", "visualization", "dashboard"]
---

# Project Overview
Tricys Visual is the Vue 3-based frontend for the TRICYS platform. It provides live monitoring, digital twin visualization, and result analysis so researchers can explore simulation outputs interactively.

## Architecture Design
### 1. Feature-based Frontend Structure
```
src/
├── api/         # API clients and service modules
├── components/  # Common, layout, and feature components
├── composables/ # Vue Composition API hooks
├── layouts/     # Page layouts
├── router/      # Vue Router configuration
├── styles/      # Themes and global styles
├── utils/       # Helper functions
└── views/       # Top-level pages
```

### 2. Visualization & Interaction Layer
- **Three.js Digital Twin**: Interactive 3D system visualization for complex component relationships.
- **Result Analysis Tools**: Integrated file viewer for HDF5, Markdown, and structured outputs.

### 3. Live Data & Dashboard Integration
- **WebSocket Monitoring**: Real-time updates of simulation KPIs and task progress.
- **GoView Integration**: Embeds low-code dashboards for large-screen operational views.

## Workflow
1. **Local Setup**: Install Node.js (v16+), run `npm install`, then `npm run dev`.
2. **Connect Backend**: Configure `VITE_API_URL` for the Tricys Backend API and `VITE_GOVIEW_URL` for dashboards.
3. **Monitor Simulations**: Use live panels and 3D views to track running tasks.
4. **Analyze Results**: Browse simulation artifacts, reports, and visual outputs.

## Ecosystem Integration
- Pulls task and data services from [[tricys-backend]].
- Visualizes models and reports produced by [[tricys]].
