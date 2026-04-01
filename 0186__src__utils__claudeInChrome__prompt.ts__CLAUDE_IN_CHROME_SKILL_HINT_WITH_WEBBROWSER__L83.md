# CLAUDE_IN_CHROME_SKILL_HINT_WITH_WEBBROWSER

- Source: `src/utils/claudeInChrome/prompt.ts`
- Symbol: `CLAUDE_IN_CHROME_SKILL_HINT_WITH_WEBBROWSER`
- Line: 83
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
**Browser Automation**: Use WebBrowser for development (dev servers, JS eval, console, screenshots). Use claude-in-chrome for the user's real Chrome when you need logged-in sessions, OAuth, or computer-use — invoke Skill(skill: "claude-in-chrome") before any mcp__claude-in-chrome__* tool.
```

## Prompt Translation

```text
**浏览器自动化**：开发时使用 `WebBrowser`（开发服务器、JS 求值、控制台、截图）。当你需要已登录会话、OAuth 或电脑操作时，使用 `claude-in-chrome` 来操作用户真实的 Chrome——在使用任何 `mcp__claude-in-chrome__*` 工具之前先调用 `Skill(skill: "claude-in-chrome")`。
```
