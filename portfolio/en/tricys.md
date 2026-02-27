---
title: "TRICYS: Tritium Integrated Cycle Simulation Platform"
date: 2026-02-27
category: "TRICYS"
description: "Open-source fusion tritium fuel cycle simulator with modular co-simulation, parameter scanning, and automated reporting."
tags: ["fusion", "simulation", "python", "modelica"]
---

# Project Overview
TRICYS (TRitium Integrated CYcle Simulation) is an open-source, modular, multi-scale simulator for fusion reactor tritium fuel cycles. It focuses on physics-based, closed-loop analysis that respects plant-wide mass conservation while enabling researchers to explore tritium management strategies at system scale.

## Architecture Design
### 1. Physics Modeling Core
- **OpenModelica + Modelica**: Core physical models are implemented with Modelica and executed by OpenModelica.
- **Dynamic System Library**: Modular components cover plasma exhaust processing, isotope separation, and fuel supply loops to compose full-cycle simulations.

### 2. Simulation Orchestration & Parameter Scanning
- **Python CLI Orchestration**: A Python-driven workflow coordinates scenario execution, batch runs, and concurrency.
- **Parameter Scans**: Built-in multi-parameter scanning enables large-scale sensitivity exploration.

### 3. Co-simulation & External Tool Bridge
- **Sub-module Co-simulation**: Data exchange interfaces allow integration with external tools (e.g., Aspen Plus) for hybrid system studies.

### 4. Analysis & Reporting Layer
- **Automated Reports**: Standardized Markdown reports compile charts, statistics, and output summaries automatically.
- **Sensitivity & AI Augmentation**: SALib-based sensitivity analysis and LLM-assisted report writing turn raw data into structured insights.

### 5. Developer Environment
- **Windows-first Setup**: Local installation for full co-simulation support.
- **Docker Dev Containers**: Containerized environments for standardized 0D simulations and reproducible development.

## Workflow
1. **Environment Setup**: Install Python (3.8+), OpenModelica, and project dependencies.
2. **Scenario Definition**: Assemble Modelica components and define parameter sets.
3. **Simulation Execution**: Run `tricys` CLI tasks or batch parameter scans.
4. **Analysis & Report**: Generate automated Markdown reports with charts, statistics, and AI summaries.
5. **Iteration**: Use sensitivity results to refine design assumptions and repeat.

## Ecosystem Integration
- Coordinates with [[tricys-backend]] for task scheduling, monitoring, and data services.
- Feeds results to [[tricys-visual]] for 3D visualization and real-time dashboards.
