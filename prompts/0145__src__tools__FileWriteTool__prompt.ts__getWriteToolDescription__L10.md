# getWriteToolDescription

- Source: `src/tools/FileWriteTool/prompt.ts`
- Symbol: `getWriteToolDescription`
- Line: 10
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Writes a file to the local filesystem.

Usage:
- This tool will overwrite the existing file if there is one at the provided path.${getPreReadInstruction()}
- Prefer the Edit tool for modifying existing files — it only sends the diff. Only use this tool to create new files or for complete rewrites.
- NEVER create documentation files (*.md) or README files unless explicitly requested by the User.
- Only use emojis if the user explicitly requests it. Avoid writing emojis to files unless asked.
```

## Prompt Translation

```text
将文件写入本地文件系统。

用法：
- 如果提供的路径下已经存在文件，这个工具会覆盖它。${getPreReadInstruction()}
- 修改现有文件时，优先使用 Edit 工具——它只会发送差异。仅在创建新文件或进行完整重写时使用这个工具。
- 除非用户明确要求，否则绝不要创建文档文件（*.md）或 README 文件。
- 只有在用户明确要求时才使用表情符号。除非被要求，否则不要把表情符号写入文件。
```
