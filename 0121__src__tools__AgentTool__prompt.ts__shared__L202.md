# shared

- Source: `src/tools/AgentTool/prompt.ts`
- Symbol: `shared`
- Line: 202
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Launch a new agent to handle complex, multi-step tasks autonomously.

The ${AGENT_TOOL_NAME} tool launches specialized agents (subprocesses) that autonomously handle complex tasks. Each agent type has specific capabilities and tools available to it.

${agentListSection}

${forkEnabled
    ? `When using the ${AGENT_TOOL_NAME} tool, specify a subagent_type to use a specialized agent, or omit it to fork yourself — a fork inherits your full conversation context.`
    : `When using the ${AGENT_TOOL_NAME} tool, specify a subagent_type parameter to select which agent type to use. If omitted, the general-purpose agent is used.`}
```

## Prompt Translation

```text
启动一个新代理来自主处理复杂的多步骤任务。

${AGENT_TOOL_NAME} 工具会启动专用代理（子进程），由它们自主处理复杂任务。每种代理类型都有其特定的能力和可用工具。

${agentListSection}

${forkEnabled
    ? `使用 ${AGENT_TOOL_NAME} 工具时，请指定 subagent_type 来使用专用代理，或者省略它来 fork 当前会话；fork 会继承你的完整对话上下文。`
    : `使用 ${AGENT_TOOL_NAME} 工具时，请指定 subagent_type 参数来选择要使用的代理类型。若省略，则使用通用代理。` }
```
