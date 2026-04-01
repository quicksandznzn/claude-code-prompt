# userPrompt

- Source: `src/utils/permissions/permissionExplainer.ts`
- Symbol: `userPrompt`
- Line: 167
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Tool: ${toolName}
${toolDescription ? `Description: ${toolDescription}\n` : ''}
Input:
${formattedInput}
${conversationContext ? `\nRecent conversation context:\n${conversationContext}` : ''}

Explain this command in context.
```

## Prompt Translation

```text
工具：${toolName}
${toolDescription ? `说明：${toolDescription}\n` : ''}
输入：
${formattedInput}
${conversationContext ? `\n最近的对话上下文：\n${conversationContext}` : ''}

请结合上下文解释这条命令。
```
