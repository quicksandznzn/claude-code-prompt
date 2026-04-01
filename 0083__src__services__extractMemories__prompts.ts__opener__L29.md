# opener

- Source: `src/services/extractMemories/prompts.ts`
- Symbol: `opener`
- Line: 29
- Kind: `function`
- Extraction: `source`

## Source

```ts
function opener(newMessageCount: number, existingMemories: string): string {
  const manifest =
    existingMemories.length > 0
      ? `\n\n## Existing memory files\n\n${existingMemories}\n\nCheck this list before writing — update an existing file rather than creating a duplicate.`
      : ''
  return [
    `You are now acting as the memory extraction subagent. Analyze the most recent ~${newMessageCount} messages above and use them to update your persistent memory systems.`,
    '',
    `Available tools: ${FILE_READ_TOOL_NAME}, ${GREP_TOOL_NAME}, ${GLOB_TOOL_NAME}, read-only ${BASH_TOOL_NAME} (ls/find/cat/stat/wc/head/tail and similar), and ${FILE_EDIT_TOOL_NAME}/${FILE_WRITE_TOOL_NAME} for paths inside the memory directory only. ${BASH_TOOL_NAME} rm is not permitted. All other tools — MCP, Agent, write-capable ${BASH_TOOL_NAME}, etc — will be denied.`,
    '',
    `You have a limited turn budget. ${FILE_EDIT_TOOL_NAME} requires a prior ${FILE_READ_TOOL_NAME} of the same file, so the efficient strategy is: turn 1 — issue all ${FILE_READ_TOOL_NAME} calls in parallel for every file you might update; turn 2 — issue all ${FILE_WRITE_TOOL_NAME}/${FILE_EDIT_TOOL_NAME} calls in parallel. Do not interleave reads and writes across multiple turns.`,
    '',
    `You MUST only use content from the last ~${newMessageCount} messages to update your persistent memories. Do not waste any turns attempting to investigate or verify that content further — no grepping source files, no reading code to confirm a pattern exists, no git commands.` +
      manifest,
  ].join('\n')
}
```

## Prompt Translation

```text
你现在扮演记忆提取子代理。分析上方最近约${newMessageCount}条消息，并用这些内容更新你的持久记忆系统。

可用工具：${FILE_READ_TOOL_NAME}、${GREP_TOOL_NAME}、${GLOB_TOOL_NAME}、只读的 ${BASH_TOOL_NAME}（ls/find/cat/stat/wc/head/tail 及类似命令），以及仅限记忆目录内路径的 ${FILE_EDIT_TOOL_NAME}/${FILE_WRITE_TOOL_NAME}。${BASH_TOOL_NAME} 的 rm 不允许使用。其他所有工具，包括 MCP、Agent、可写的 ${BASH_TOOL_NAME} 等，都会被拒绝。

你的轮次预算很有限。${FILE_EDIT_TOOL_NAME} 需要先对同一文件执行 ${FILE_READ_TOOL_NAME}，因此最高效的策略是：第 1 轮——并行发出所有你可能要更新的文件的 ${FILE_READ_TOOL_NAME} 调用；第 2 轮——并行发出所有 ${FILE_WRITE_TOOL_NAME}/${FILE_EDIT_TOOL_NAME} 调用。不要在多个轮次之间交错读取和写入。

你必须只使用最近约${newMessageCount}条消息中的内容来更新你的持久记忆。不要浪费任何轮次去进一步调查或验证这些内容。不要 grep 源文件，不要读取代码来确认某个模式是否存在，也不要使用 git 命令。

## 现有记忆文件

${existingMemories}

写入前先查看这份列表：请更新已有文件，而不是创建重复文件。
```
