# CHROME_TOOL_SEARCH_INSTRUCTIONS

- Source: `src/utils/claudeInChrome/prompt.ts`
- Symbol: `CHROME_TOOL_SEARCH_INSTRUCTIONS`
- Line: 53
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
**IMPORTANT: Before using any chrome browser tools, you MUST first load them using ToolSearch.**

Chrome browser tools are MCP tools that require loading before use. Before calling any mcp__claude-in-chrome__* tool:
1. Use ToolSearch with `select:mcp__claude-in-chrome__<tool_name>` to load the specific tool
2. Then call the tool

For example, to get tab context:
1. First: ToolSearch with query "select:mcp__claude-in-chrome__tabs_context_mcp"
2. Then: Call mcp__claude-in-chrome__tabs_context_mcp
```

## Prompt Translation

```text
**重要：在使用任何 Chrome 浏览器工具之前，你必须先使用 ToolSearch 将它们加载。**

Chrome 浏览器工具是需要先加载才能使用的 MCP 工具。在调用任何 `mcp__claude-in-chrome__*` 工具之前：
1. 使用 `select:mcp__claude-in-chrome__<tool_name>` 的 ToolSearch 来加载对应工具
2. 然后调用该工具

例如，要获取标签页上下文：
1. 首先：使用查询 "select:mcp__claude-in-chrome__tabs_context_mcp" 的 ToolSearch
2. 然后：调用 `mcp__claude-in-chrome__tabs_context_mcp`
```
