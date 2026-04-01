# INSIGHT_SECTIONS.prompt

- Source: `src/commands/insights.ts`
- Symbol: `INSIGHT_SECTIONS.prompt`
- Line: 1353
- Kind: `property`
- Extraction: `text`

## Prompt

```text
Analyze this Claude Code usage data and describe the user's interaction style.

RESPOND WITH ONLY A VALID JSON OBJECT:
{
  "narrative": "2-3 paragraphs analyzing HOW the user interacts with Claude Code. Use second person 'you'. Describe patterns: iterate quickly vs detailed upfront specs? Interrupt often or let Claude run? Include specific examples. Use **bold** for key insights.",
  "key_pattern": "One sentence summary of most distinctive interaction style"
}
```

## Prompt Translation

```text
分析这份 Claude Code 使用数据，并描述用户的交互风格。

仅使用一个有效的 JSON 对象回复：
{
  "narrative": "用 2-3 段分析用户如何与 Claude Code 交互。使用第二人称“你”。描述模式：是快速迭代还是先给出详细规格？是经常打断还是让 Claude 自行运行？请包含具体示例。用 **粗体** 标出关键洞察。",
  "key_pattern": "用一句话概括最具辨识度的交互风格"
}
```
