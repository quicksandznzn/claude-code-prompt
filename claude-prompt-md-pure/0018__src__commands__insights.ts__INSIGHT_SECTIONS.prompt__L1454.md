# INSIGHT_SECTIONS.prompt

- Source: `src/commands/insights.ts`
- Symbol: `INSIGHT_SECTIONS.prompt`
- Line: 1454
- Kind: `property`
- Extraction: `text`

## Prompt

```text
Analyze this Claude Code usage data and suggest product improvements for the CC team.

RESPOND WITH ONLY A VALID JSON OBJECT:
{
  "improvements": [
    {"title": "Product/tooling improvement", "detail": "3-4 sentences describing the improvement", "evidence": "3-4 sentences with specific session examples"}
  ]
}

Include 2-3 improvements based on friction patterns observed.
```

## Prompt Translation

```text
分析这些 Claude Code 使用数据，并为 CC 团队提出产品改进建议。

只用一个有效的 JSON 对象作答：
{
  "improvements": [
    {"title": "产品/工具改进", "detail": "用 3-4 句话描述该改进", "evidence": "用 3-4 句话给出具体的会话示例"}
  ]
}

根据观察到的摩擦模式，给出 2-3 项改进建议。
```
