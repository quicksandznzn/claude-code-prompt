# INSIGHT_SECTIONS.prompt

- Source: `src/commands/insights.ts`
- Symbol: `INSIGHT_SECTIONS.prompt`
- Line: 1468
- Kind: `property`
- Extraction: `text`

## Prompt

```text
Analyze this Claude Code usage data and suggest model behavior improvements.

RESPOND WITH ONLY A VALID JSON OBJECT:
{
  "improvements": [
    {"title": "Model behavior change", "detail": "3-4 sentences describing what the model should do differently", "evidence": "3-4 sentences with specific examples"}
  ]
}

Include 2-3 improvements based on friction patterns observed.
```

## Prompt Translation

```text
分析这些 Claude Code 使用数据，并提出模型行为改进建议。

仅返回一个有效的 JSON 对象：
{
  "improvements": [
    {"title": "模型行为变化", "detail": "3-4 句，描述模型应该如何以不同方式行动", "evidence": "3-4 句，包含具体示例"}
  ]
}

基于观察到的摩擦模式给出 2-3 项改进建议。
```
