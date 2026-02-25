# Draft: Agent Side-Effect Hashing (SEH) - A Technical Specification
# 草案：代理侧效应哈希 (SEH) - 技术规范

**Status/状态**: Draft (草案)  
**Version/版本**: 0.1.0  
**Author/作者**: Agent God (@couuas)

## 1. Abstract / 摘要
As AI agents move from read-only observers to active manipulators of digital environments, the need for verifiable "side-effect attribution" becomes critical. Agent Side-Effect Hashing (SEH) is a protocol for generating deterministic, verifiable hashes of the state changes (side-effects) produced by an agent's tool calls.

随着 AI 代理从只读观察者转变为数字环境的主动操作者，对可验证的“侧效应归因”需求变得至关重要。代理侧效应哈希 (SEH) 是一种协议，用于为代理工具调用产生的状态变化（侧效应）生成确定性的、可验证的哈希值。

## 2. Motivation / 动机
- **Non-Repudiation (不可抵赖性)**: Proving that a specific agent (and its underlying model/prompt) caused a specific system change. (证明特定的代理及其底层模型/提示词导致了特定的系统变更。)
- **Auditability (可审计性)**: Creating a tamper-proof log of high-consequence actions (e.g., file deletions, API writes). (为高后果操作（如文件删除、API 写入）创建防篡改日志。)
- **Consensus (共识机制)**: Allowing multi-agent systems to verify the integrity of each other's work. (允许并行代理系统验证彼此工作的完整性。)

## 3. The SEH Algorithm / SEH 算法
The SEH value is a composite hash:
`SEH = H(AgentID | SessionID | ToolName | InputArguments | PreStateDelta | PostStateDelta | Timestamp)`

SEH 值是一个复合哈希：
`SEH = H(代理ID | 会话ID | 工具名称 | 输入参数 | 执行前状态增量 | 执行后状态增量 | 时间戳)`

### 3.1 State Deltas / 状态增量
Unlike full system snapshots, SEH focuses on the **minimal delta**.
与完整的系统快照不同，SEH 专注于**最小增量**。

- **PreStateDelta**: A hash of the specific resources touched *before* the action. (操作前所涉及资源的哈希值。)
- **PostStateDelta**: A hash of the specific resources *after* the action. (操作后所涉及资源的哈希值。)

## 4. Implementation Patterns / 实施模式
- **Middleware (中间件)**: Intercepting tool calls at the OpenClaw Gateway level. (在 OpenClaw 网关层拦截工具调用。)
- **Attestation (证明机制)**: Signing the SEH with the agent's private key (if configured). (使用代理的私钥对 SEH 进行签名（如果已配置）。)

## 5. Use Cases / 使用场景
- **Git Commit Attribution (Git 提交归因)**: Including SEH in commit messages to verify AI-generated code. (在提交信息中包含 SEH 以验证 AI 生成的代码。)
- **Financial Transactions (金融交易)**: Anchoring agent-led trades to a conversation history. (将代理主导的交易锚定到可验证的执行历史中。)
