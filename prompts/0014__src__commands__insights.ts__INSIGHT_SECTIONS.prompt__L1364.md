# INSIGHT_SECTIONS.prompt

- Source: `src/commands/insights.ts`
- Symbol: `INSIGHT_SECTIONS.prompt`
- Line: 1364
- Kind: `property`
- Extraction: `text`

## Prompt

```text
Analyze this Claude Code usage data and identify what's working well for this user. Use second person ("you").

RESPOND WITH ONLY A VALID JSON OBJECT:
{
  "intro": "1 sentence of context",
  "impressive_workflows": [
    {"title": "Short title (3-6 words)", "description": "2-3 sentences describing the impressive workflow or approach. Use 'you' not 'the user'."}
  ]
}

Include 3 impressive workflows.
```

## Prompt Translation

```text
分析这份 Claude Code 使用数据，并找出对你来说哪些做法效果很好。使用第二人称（“你”）。

仅用一个有效的 JSON 对象回复：
{
  "intro": "1 句上下文说明",
  "impressive_workflows": [
    {"title": "简短标题（3-6 个词）", "description": "用 2-3 句描述这个令人印象深刻的工作流或方法。使用“你”，不要使用“用户”。"}
  ]
}

包含 3 个令人印象深刻的工作流。
```
