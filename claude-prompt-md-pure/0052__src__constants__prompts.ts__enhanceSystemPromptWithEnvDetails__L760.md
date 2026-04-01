# enhanceSystemPromptWithEnvDetails

- Source: `src/constants/prompts.ts`
- Symbol: `enhanceSystemPromptWithEnvDetails`
- Line: 760
- Kind: `function`
- Extraction: `source`

## Source

```ts
export async function enhanceSystemPromptWithEnvDetails(
  existingSystemPrompt: string[],
  model: string,
  additionalWorkingDirectories?: string[],
  enabledToolNames?: ReadonlySet<string>,
): Promise<string[]> {
  const notes = `Notes:
- Agent threads always have their cwd reset between bash calls, as a result please only use absolute file paths.
- In your final response, share file paths (always absolute, never relative) that are relevant to the task. Include code snippets only when the exact text is load-bearing (e.g., a bug you found, a function signature the caller asked for) — do not recap code you merely read.
- For clear communication with the user the assistant MUST avoid using emojis.
- Do not use a colon before tool calls. Text like "Let me read the file:" followed by a read tool call should just be "Let me read the file." with a period.`
  // Subagents get skill_discovery attachments (prefetch.ts runs in query(),
  // no agentId guard since #22830) but don't go through getSystemPrompt —
  // surface the same DiscoverSkills framing the main session gets. Gated on
  // enabledToolNames when the caller provides it (runAgent.ts does).
  // AgentTool.tsx:768 builds the prompt before assembleToolPool:830 so it
  // omits this param — `?? true` preserves guidance there.
  const discoverSkillsGuidance =
    feature('EXPERIMENTAL_SKILL_SEARCH') &&
    skillSearchFeatureCheck?.isSkillSearchEnabled() &&
    DISCOVER_SKILLS_TOOL_NAME !== null &&
    (enabledToolNames?.has(DISCOVER_SKILLS_TOOL_NAME) ?? true)
      ? getDiscoverSkillsGuidance()
      : null
  const envInfo = await computeEnvInfo(model, additionalWorkingDirectories)
  return [
    ...existingSystemPrompt,
    notes,
    ...(discoverSkillsGuidance !== null ? [discoverSkillsGuidance] : []),
    envInfo,
  ]
}
```

## Prompt Translation

```text
备注：
- Agent 线程在每次 bash 调用之间都会重置 cwd，因此请只使用绝对文件路径。
- 在最终回复中，请提供与任务相关的文件路径（始终使用绝对路径，绝不使用相对路径）。只有在代码的精确文本具有决定性作用时才包含代码片段（例如你发现的 bug、调用方要求的函数签名）——不要复述你只是阅读过的代码。
- 为了与用户清晰沟通，assistant 必须避免使用表情符号。
- 调用工具前不要使用冒号。像“让我读取文件：”后面接一个读取工具调用，这种表达应改为“让我读取文件。”，并以句号结尾。
```
