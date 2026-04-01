# getDefaultEditDescription

- Source: `src/tools/FileEditTool/prompt.ts`
- Symbol: `getDefaultEditDescription`
- Line: 12
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Performs exact string replacements in files.

Usage:${getPreReadInstruction()}
- When editing text from Read tool output, ensure you preserve the exact indentation (tabs/spaces) as it appears AFTER the line number prefix. The line number prefix format is: ${prefixFormat}. Everything after that is the actual file content to match. Never include any part of the line number prefix in the old_string or new_string.
- ALWAYS prefer editing existing files in the codebase. NEVER write new files unless explicitly required.
- Only use emojis if the user explicitly requests it. Avoid adding emojis to files unless asked.
- The edit will FAIL if `old_string` is not unique in the file. Either provide a larger string with more surrounding context to make it unique or use `replace_all` to change every instance of `old_string`.${minimalUniquenessHint}
- Use `replace_all` for replacing and renaming strings across the file. This parameter is useful if you want to rename a variable for instance.
```

## Prompt Translation

```text
在文件中执行精确的字符串替换。

用法：${getPreReadInstruction()}
- 在编辑来自 Read 工具输出的文本时，请确保保留其在行号前缀之后所显示的精确缩进（tabs/spaces）。行号前缀的格式为：${prefixFormat}。这之后的所有内容才是需要匹配的实际文件内容。切勿在 `old_string` 或 `new_string` 中包含行号前缀的任何部分。
- 始终优先编辑代码库中已有的文件。除非明确要求，否则绝不要新建文件。
- 只有在用户明确请求时才使用 emoji。除非被要求，否则不要在文件中添加 emoji。
- 如果 `old_string` 在文件中不唯一，编辑将会失败。请提供更长、上下文更多的字符串以使其唯一，或者使用 `replace_all` 来替换 `old_string` 的每一个实例。${minimalUniquenessHint}
- 使用 `replace_all` 在整个文件中替换和重命名字符串。如果你想重命名某个变量，这个参数会很有用。
```
