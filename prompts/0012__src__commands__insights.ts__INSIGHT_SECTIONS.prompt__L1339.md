# INSIGHT_SECTIONS.prompt

- Source: `src/commands/insights.ts`
- Symbol: `INSIGHT_SECTIONS.prompt`
- Line: 1339
- Kind: `property`
- Extraction: `text`

## Prompt

```text
Analyze this Claude Code usage data and identify project areas.

RESPOND WITH ONLY A VALID JSON OBJECT:
{
  "areas": [
    {"name": "Area name", "session_count": N, "description": "2-3 sentences about what was worked on and how Claude Code was used."}
  ]
}

Include 4-5 areas. Skip internal CC operations.
```

## Prompt Translation

```text
分析这份 Claude Code 使用数据并识别项目领域。

仅使用合法的 JSON 对象作答：
{
  "areas": [
    {"name": "领域名称", "session_count": N, "description": "关于做了什么以及 Claude Code 如何被使用的 2-3 句说明。"}
  ]
}

包含 4-5 个领域。跳过内部 CC 操作。
```
