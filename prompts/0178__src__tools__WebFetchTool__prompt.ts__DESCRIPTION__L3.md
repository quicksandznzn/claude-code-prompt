# DESCRIPTION

- Source: `src/tools/WebFetchTool/prompt.ts`
- Symbol: `DESCRIPTION`
- Line: 3
- Kind: `variable`
- Extraction: `text`

## Prompt

```text

- Fetches content from a specified URL and processes it using an AI model
- Takes a URL and a prompt as input
- Fetches the URL content, converts HTML to markdown
- Processes the content with the prompt using a small, fast model
- Returns the model's response about the content
- Use this tool when you need to retrieve and analyze web content

Usage notes:
  - IMPORTANT: If an MCP-provided web fetch tool is available, prefer using that tool instead of this one, as it may have fewer restrictions.
  - The URL must be a fully-formed valid URL
  - HTTP URLs will be automatically upgraded to HTTPS
  - The prompt should describe what information you want to extract from the page
  - This tool is read-only and does not modify any files
  - Results may be summarized if the content is very large
  - Includes a self-cleaning 15-minute cache for faster responses when repeatedly accessing the same URL
  - When a URL redirects to a different host, the tool will inform you and provide the redirect URL in a special format. You should then make a new WebFetch request with the redirect URL to fetch the content.
  - For GitHub URLs, prefer using the gh CLI via Bash instead (e.g., gh pr view, gh issue view, gh api).
```

## Prompt Translation

```text

- 从指定 URL 获取内容，并使用 AI 模型进行处理
- 接受 URL 和提示词作为输入
- 获取 URL 内容，将 HTML 转为 markdown
- 使用小型、快速模型结合提示词处理内容
- 返回模型对该内容的回答
- 在需要检索和分析网页内容时使用此工具

使用说明：
  - 重要：如果有 MCP 提供的 web fetch 工具可用，优先使用它而不是这个工具，因为它可能限制更少。
  - URL 必须是格式完整且有效的 URL
  - HTTP URL 会自动升级为 HTTPS
  - 提示词应描述你想从页面提取哪些信息
  - 此工具是只读的，不会修改任何文件
  - 如果内容非常大，结果可能会被摘要
  - 包含一个会自动清理的 15 分钟缓存，以便重复访问同一 URL 时获得更快响应
  - 当某个 URL 重定向到不同的主机时，工具会通知你，并以特殊格式提供重定向后的 URL。然后你应该使用该重定向 URL 发起新的 WebFetch 请求来获取内容。
  - 对于 GitHub URL，优先改用 Bash 通过 gh CLI（例如 `gh pr view`、`gh issue view`、`gh api`）。
```
