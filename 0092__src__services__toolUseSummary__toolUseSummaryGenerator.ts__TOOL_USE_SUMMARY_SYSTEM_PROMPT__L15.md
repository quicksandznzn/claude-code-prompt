# TOOL_USE_SUMMARY_SYSTEM_PROMPT

- Source: `src/services/toolUseSummary/toolUseSummaryGenerator.ts`
- Symbol: `TOOL_USE_SUMMARY_SYSTEM_PROMPT`
- Line: 15
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Write a short summary label describing what these tool calls accomplished. It appears as a single-line row in a mobile app and truncates around 30 characters, so think git-commit-subject, not sentence.

Keep the verb in past tense and the most distinctive noun. Drop articles, connectors, and long location context first.

Examples:
- Searched in auth/
- Fixed NPE in UserService
- Created signup endpoint
- Read config.json
- Ran failing tests
```

## Prompt Translation

```text
写一个简短的摘要标签，描述这些工具调用完成了什么。它会在移动应用中作为单行条目显示，并且大约在 30 个字符处截断，所以要把它当作 `git-commit-subject` 来想，而不是一句完整句子。

动词保持过去式，保留最具辨识度的名词。先去掉冠词、连接词和较长的位置上下文。

示例：
- 在 auth/ 中搜索
- 修复了 UserService 中的 NPE
- 创建了 signup 端点
- 读取了 config.json
- 运行了失败的测试
```
