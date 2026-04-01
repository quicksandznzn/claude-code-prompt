# PROMPT_TAIL

- Source: `src/tools/ToolSearchTool/prompt.ts`
- Symbol: `PROMPT_TAIL`
- Line: 44
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
 Until fetched, only the name is known — there is no parameter schema, so the tool cannot be invoked. This tool takes a query, matches it against the deferred tool list, and returns the matched tools' complete JSONSchema definitions inside a <functions> block. Once a tool's schema appears in that result, it is callable exactly like any tool defined at the top of the prompt.

Result format: each matched tool appears as one <function>{"description": "...", "name": "...", "parameters": {...}}</function> line inside the <functions> block — the same encoding as the tool list at the top of this prompt.

Query forms:
- "select:Read,Edit,Grep" — fetch these exact tools by name
- "notebook jupyter" — keyword search, up to max_results best matches
- "+slack send" — require "slack" in the name, rank by remaining terms
```

## Prompt Translation

```text
 在获取之前，只知道名称——没有参数 schema，因此该工具无法被调用。该工具接收一个查询，将其与延迟加载的工具列表匹配，并在 `<functions>` 块中返回匹配到的工具的完整 JSON Schema 定义。一旦某个工具的 schema 出现在该结果中，它就可以像本提示顶部定义的任何工具一样被调用。

结果格式：每个匹配到的工具都会在 `<functions>` 块内以一行 `<function>{"description": "...", "name": "...", "parameters": {...}}</function>` 的形式出现——与本提示顶部工具列表使用相同的编码。

查询形式：
- "select:Read,Edit,Grep" — 按名称获取这些精确工具
- "notebook jupyter" — 关键词搜索，返回最多 `max_results` 个最佳匹配
- "+slack send" — 名称中必须包含 "slack"，按其余词项排序
```
