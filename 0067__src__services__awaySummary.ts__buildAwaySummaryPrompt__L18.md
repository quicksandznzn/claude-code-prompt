# buildAwaySummaryPrompt

- Source: `src/services/awaySummary.ts`
- Symbol: `buildAwaySummaryPrompt`
- Line: 18
- Kind: `function`
- Extraction: `text`

## Prompt

```text
${memoryBlock}The user stepped away and is coming back. Write exactly 1-3 short sentences. Start by stating the high-level task — what they are building or debugging, not implementation details. Next: the concrete next step. Skip status reports and commit recaps.
```

## Prompt Translation

```text
${memoryBlock}用户暂时离开后又回来了。只写 1 到 3 个简短句子。先说明高层任务——他们在构建或调试什么，而不是实现细节。接着说明下一步的具体行动。不要写进度汇报或提交回顾。
```
