# baseInstructions

- Source: `src/utils/mcpOutputStorage.ts`
- Symbol: `baseInstructions`
- Line: 45
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Error: result (${contentLength.toLocaleString()} characters) exceeds maximum allowed tokens. Output has been saved to ${rawOutputPath}.
Format: ${formatDescription}
Use offset and limit parameters to read specific portions of the file, search within it for specific content, and jq to make structured queries.
REQUIREMENTS FOR SUMMARIZATION/ANALYSIS/REVIEW:
- You MUST read the content from the file at ${rawOutputPath} in sequential chunks until 100% of the content has been read.
```

## Prompt Translation

```text
错误：结果（${contentLength.toLocaleString()} 个字符）超过了允许的最大 token 数。输出已保存到 ${rawOutputPath}。
格式：${formatDescription}
使用 offset 和 limit 参数读取文件的特定部分，在其中搜索特定内容，并使用 jq 进行结构化查询。
总结/分析/审查要求：
- 你必须从 ${rawOutputPath} 文件中按顺序分块读取内容，直到 100% 的内容都已读取。
```
