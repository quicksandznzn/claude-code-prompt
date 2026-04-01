# getDescription

- Source: `src/tools/GrepTool/prompt.ts`
- Symbol: `getDescription`
- Line: 6
- Kind: `function`
- Extraction: `text`

## Prompt

```text
A powerful search tool built on ripgrep

  Usage:
  - ALWAYS use ${GREP_TOOL_NAME} for search tasks. NEVER invoke `grep` or `rg` as a ${BASH_TOOL_NAME} command. The ${GREP_TOOL_NAME} tool has been optimized for correct permissions and access.
  - Supports full regex syntax (e.g., "log.*Error", "function\s+\w+")
  - Filter files with glob parameter (e.g., "*.js", "**/*.tsx") or type parameter (e.g., "js", "py", "rust")
  - Output modes: "content" shows matching lines, "files_with_matches" shows only file paths (default), "count" shows match counts
  - Use ${AGENT_TOOL_NAME} tool for open-ended searches requiring multiple rounds
  - Pattern syntax: Uses ripgrep (not grep) - literal braces need escaping (use `interface\{\}` to find `interface{}` in Go code)
  - Multiline matching: By default patterns match within single lines only. For cross-line patterns like `struct \{[\s\S]*?field`, use `multiline: true`
```

## Prompt Translation

```text
基于 ripgrep 构建的强大搜索工具

  用法：
  - 进行搜索任务时，始终使用 ${GREP_TOOL_NAME}。绝不要将 `grep` 或 `rg` 作为 ${BASH_TOOL_NAME} 命令调用。${GREP_TOOL_NAME} 工具已针对正确的权限和访问进行了优化。
  - 支持完整的正则语法（例如，"log.*Error"、"function\s+\w+"）
  - 可通过 glob 参数过滤文件（例如，"*.js"、"**/*.tsx"），或通过 type 参数过滤（例如，"js"、"py"、"rust"）
  - 输出模式："content" 显示匹配行，"files_with_matches" 仅显示文件路径（默认），"count" 显示匹配次数
  - 对于需要多轮交互的开放式搜索，请使用 ${AGENT_TOOL_NAME} 工具
  - 模式语法：使用的是 ripgrep（不是 grep）- 需要对字面量大括号进行转义（例如，在 Go 代码中查找 `interface{}` 时使用 `interface\{\}`）
  - 多行匹配：默认情况下，模式只会在单行内匹配。对于跨行模式，例如 `struct \{[\s\S]*?field`，请使用 `multiline: true`
```
