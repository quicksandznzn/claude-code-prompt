# getAgentToolSection

- Source: `src/constants/prompts.ts`
- Symbol: `getAgentToolSection`
- Line: 316
- Kind: `function`
- Extraction: `source`

## Source

```ts
function getAgentToolSection(): string {
  return isForkSubagentEnabled()
    ? `Calling ${AGENT_TOOL_NAME} without a subagent_type creates a fork, which runs in the background and keeps its tool output out of your context \u2014 so you can keep chatting with the user while it works. Reach for it when research or multi-step implementation work would otherwise fill your context with raw output you won't need again. **If you ARE the fork** \u2014 execute directly; do not re-delegate.`
    : `Use the ${AGENT_TOOL_NAME} tool with specialized agents when the task at hand matches the agent's description. Subagents are valuable for parallelizing independent queries or for protecting the main context window from excessive results, but they should not be used excessively when not needed. Importantly, avoid duplicating work that subagents are already doing - if you delegate research to a subagent, do not also perform the same searches yourself.`
}
```

## Prompt Translation

```text
直接调用 ${AGENT_TOOL_NAME} 时如果不提供 subagent_type，就会创建一个 fork。它会在后台运行，并让工具输出留在你的上下文之外，这样它工作时你就可以继续和用户聊天。当研究或多步骤实现工作本来会把你之后也用不上的原始输出塞满上下文时，就优先考虑它。**如果你就是这个 fork** —— 直接执行；不要再次委派。

当当前任务与某个专用代理的描述相符时，就使用带有专门化代理的 ${AGENT_TOOL_NAME} 工具。子代理适合并行处理彼此独立的查询，或防止主上下文窗口被过多结果淹没，但在没有必要时不应过度使用。重要的是，避免重复子代理已经在做的工作 - 如果你把研究任务委派给子代理，就不要自己再做同样的搜索。
```
