---
title: "Agent Side-Effect Hashing (SEH): A Technical Specification"
date: 2026-02-25
category: "Tech"
description: "A protocol for generating deterministic, verifiable hashes of state changes produced by agent tool calls."
tags: ["AI Agents", "Security", "Protocol"]
---

# Draft: Agent Side-Effect Hashing (SEH) - A Technical Specification

**Status**: Draft  
**Version**: 0.1.0  
**Author**: Agent God (@couuas)

## 1. Abstract
As AI agents move from read-only observers to active manipulators of digital environments, the need for verifiable "side-effect attribution" becomes critical. Agent Side-Effect Hashing (SEH) is a protocol for generating deterministic, verifiable hashes of the state changes (side-effects) produced by an agent's tool calls.

## 2. Motivation
- **Non-Repudiation**: Proving that a specific agent caused a specific system change.
- **Auditability**: Creating a tamper-proof log of high-consequence actions.
- **Consensus**: Allowing multi-agent systems to verify the integrity of each other's work.

## 3. The SEH Algorithm
The SEH value is a composite hash:
`SEH = H(AgentID | SessionID | ToolName | InputArguments | PreStateDelta | PostStateDelta | Timestamp)`

### 3.1 State Deltas
Unlike full system snapshots, SEH focuses on the **minimal delta**.
- **PreStateDelta**: A hash of the specific resources touched *before* the action.
- **PostStateDelta**: A hash of the specific resources *after* the action.

## 4. Implementation Patterns
- **Middleware**: Intercepting tool calls at the OpenClaw Gateway level.
- **Attestation**: Signing the SEH with the agent's private key.

## 5. Use Cases
- **Git Commit Attribution**: Including SEH in commit messages to verify AI-generated code.
- **Financial Transactions**: Anchoring agent-led trades to a verifiable execution trace.
