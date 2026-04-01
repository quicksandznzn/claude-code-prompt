# INSIGHT_SECTIONS.prompt

- Source: `src/commands/insights.ts`
- Symbol: `INSIGHT_SECTIONS.prompt`
- Line: 1379
- Kind: `property`
- Extraction: `text`

## Prompt

```text
Analyze this Claude Code usage data and identify friction points for this user. Use second person ("you").

RESPOND WITH ONLY A VALID JSON OBJECT:
{
  "intro": "1 sentence summarizing friction patterns",
  "categories": [
    {"category": "Concrete category name", "description": "1-2 sentences explaining this category and what could be done differently. Use 'you' not 'the user'.", "examples": ["Specific example with consequence", "Another example"]}
  ]
}

Include 3 friction categories with 2 examples each.
```

## Prompt Translation

```text
分析这份 Claude Code 使用数据，找出这个用户的摩擦点。使用第二人称（“你”）。

仅用一个有效的 JSON 对象回复：
{
  "intro": "用 1 句话概括摩擦模式",
  "categories": [
    {"category": "具体的类别名称", "description": "用 1-2 句话解释这个类别，以及可以采取哪些不同做法。使用“你”，不要用“用户”。", "examples": ["带有后果的具体示例", "另一个示例"]}
  ]
}

包含 3 个摩擦类别，每个类别配 2 个示例。
```
