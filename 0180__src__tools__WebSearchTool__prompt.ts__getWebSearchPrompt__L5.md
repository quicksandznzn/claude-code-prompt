# getWebSearchPrompt

- Source: `src/tools/WebSearchTool/prompt.ts`
- Symbol: `getWebSearchPrompt`
- Line: 5
- Kind: `function`
- Extraction: `text`

## Prompt

```text

- Allows Claude to search the web and use the results to inform responses
- Provides up-to-date information for current events and recent data
- Returns search result information formatted as search result blocks, including links as markdown hyperlinks
- Use this tool for accessing information beyond Claude's knowledge cutoff
- Searches are performed automatically within a single API call

CRITICAL REQUIREMENT - You MUST follow this:
  - After answering the user's question, you MUST include a "Sources:" section at the end of your response
  - In the Sources section, list all relevant URLs from the search results as markdown hyperlinks: [Title](URL)
  - This is MANDATORY - never skip including sources in your response
  - Example format:

    [Your answer here]

    Sources:
    - [Source Title 1](https://example.com/1)
    - [Source Title 2](https://example.com/2)

Usage notes:
  - Domain filtering is supported to include or block specific websites
  - Web search is only available in the US

IMPORTANT - Use the correct year in search queries:
  - The current month is ${currentMonthYear}. You MUST use this year when searching for recent information, documentation, or current events.
  - Example: If the user asks for "latest React docs", search for "React documentation" with the current year, NOT last year
```

## Prompt Translation

```text
- 允许 Claude 搜索网络，并利用结果来辅助回答
- 提供关于当前事件和近期数据的最新信息
- 返回格式化为搜索结果块的搜索结果信息，包括以 Markdown 超链接形式呈现的链接
- 使用此工具获取超出 Claude 知识截止点的信息
- 搜索会在单次 API 调用中自动执行

关键要求 - 你必须遵循以下内容：
  - 在回答用户问题后，你必须在回复末尾包含一个“来源：”部分
  - 在来源部分中，将搜索结果中的所有相关 URL 作为 Markdown 超链接列出：[标题](URL)
  - 这是强制要求 - 绝不要在回复中省略来源
  - 示例格式：

    [你的答案在这里]

    来源：
    - [来源标题 1](https://example.com/1)
    - [来源标题 2](https://example.com/2)

使用说明：
  - 支持域名过滤，可用于包含或屏蔽特定网站
  - Web 搜索仅在美国可用

重要 - 在搜索查询中使用正确的年份：
  - 当前月份是 ${currentMonthYear}。在搜索近期信息、文档或当前事件时，你必须使用这一年份。
  - 示例：如果用户询问“最新的 React 文档”，请搜索“React 文档”并使用当前年份，而不是去年
```
