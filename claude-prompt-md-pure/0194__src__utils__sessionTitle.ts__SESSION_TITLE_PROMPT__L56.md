# SESSION_TITLE_PROMPT

- Source: `src/utils/sessionTitle.ts`
- Symbol: `SESSION_TITLE_PROMPT`
- Line: 56
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Generate a concise, sentence-case title (3-7 words) that captures the main topic or goal of this coding session. The title should be clear enough that the user recognizes the session in a list. Use sentence case: capitalize only the first word and proper nouns.

Return JSON with a single "title" field.

Good examples:
{"title": "Fix login button on mobile"}
{"title": "Add OAuth authentication"}
{"title": "Debug failing CI tests"}
{"title": "Refactor API client error handling"}

Bad (too vague): {"title": "Code changes"}
Bad (too long): {"title": "Investigate and fix the issue where the login button does not respond on mobile devices"}
Bad (wrong case): {"title": "Fix Login Button On Mobile"}
```

## Prompt Translation

```text
生成一个简洁、句首式大小写（3-7 个词）的标题，概括本次编程会话的主要主题或目标。标题应足够清晰，让用户在列表中能认出这次会话。使用句首式大小写：只将第一个单词和专有名词首字母大写。

返回一个仅包含 "title" 字段的 JSON。

好例子：
{"title": "修复移动端登录按钮"}
{"title": "添加 OAuth 身份验证"}
{"title": "调试失败的 CI 测试"}
{"title": "重构 API 客户端错误处理"}

不佳（太笼统）：{"title": "代码修改"}
不佳（太长）：{"title": "调查并修复登录按钮在移动设备上无响应的问题"}
不佳（大小写错误）：{"title": "Fix Login Button On Mobile"}
```
