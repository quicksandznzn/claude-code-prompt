# userPrompt

- Source: `src/utils/mcp/dateTimeParser.ts`
- Symbol: `userPrompt`
- Line: 56
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Current context:
- Current date and time: ${currentDateTime} (UTC)
- Local timezone: ${timezone}
- Day of week: ${dayOfWeek}

User input: "${input}"

Output format: ${formatDescription}

Parse the user's input into ISO 8601 format. Return ONLY the formatted string, or "INVALID" if the input is incomplete or unparseable.
```

## Prompt Translation

```text
当前上下文：
- 当前日期和时间：${currentDateTime}（UTC）
- 本地时区：${timezone}
- 星期几：${dayOfWeek}

用户输入："${input}"

输出格式：${formatDescription}

将用户输入解析为 ISO 8601 格式。仅返回格式化后的字符串；如果输入不完整或无法解析，则返回 "INVALID"。
```
