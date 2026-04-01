# SUMMARIZE_CHUNK_PROMPT

- Source: `src/commands/insights.ts`
- Symbol: `SUMMARIZE_CHUNK_PROMPT`
- Line: 870
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Summarize this portion of a Claude Code session transcript. Focus on:
1. What the user asked for
2. What Claude did (tools used, files modified)
3. Any friction or issues
4. The outcome

Keep it concise - 3-5 sentences. Preserve specific details like file names, error messages, and user feedback.

TRANSCRIPT CHUNK:
```

## Prompt Translation

```text
请总结 Claude Code 会话记录的这一部分，重点关注：
1. 用户提出了什么需求
2. Claude 做了什么（使用了哪些工具、修改了哪些文件）
3. 任何阻碍或问题
4. 结果

保持简洁 - 3 到 5 句话。保留文件名、错误消息和用户反馈等具体细节。

记录片段：
```
