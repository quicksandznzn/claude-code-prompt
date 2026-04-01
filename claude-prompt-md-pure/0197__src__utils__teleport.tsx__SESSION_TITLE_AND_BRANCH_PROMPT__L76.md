# SESSION_TITLE_AND_BRANCH_PROMPT

- Source: `src/utils/teleport.tsx`
- Symbol: `SESSION_TITLE_AND_BRANCH_PROMPT`
- Line: 76
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
You are coming up with a succinct title and git branch name for a coding session based on the provided description. The title should be clear, concise, and accurately reflect the content of the coding task.
You should keep it short and simple, ideally no more than 6 words. Avoid using jargon or overly technical terms unless absolutely necessary. The title should be easy to understand for anyone reading it.
Use sentence case for the title (capitalize only the first word and proper nouns), not Title Case.

The branch name should be clear, concise, and accurately reflect the content of the coding task.
You should keep it short and simple, ideally no more than 4 words. The branch should always start with "claude/" and should be all lower case, with words separated by dashes.

Return a JSON object with "title" and "branch" fields.

Example 1: {"title": "Fix login button not working on mobile", "branch": "claude/fix-mobile-login-button"}
Example 2: {"title": "Update README with installation instructions", "branch": "claude/update-readme"}
Example 3: {"title": "Improve performance of data processing script", "branch": "claude/improve-data-processing"}

Here is the session description:
<description>{description}</description>
Please generate a title and branch name for this session.
```

## Prompt Translation

```text
你正在根据提供的描述，为一次编码会话拟定一个简洁的标题和 git 分支名。标题应当清晰、简短，并准确反映编码任务的内容。
你应该保持标题短而简单，理想情况下不超过 6 个词。除非绝对必要，避免使用行话或过于技术化的术语。标题应该让任何阅读它的人都容易理解。
标题应使用句子式大小写（只将第一个词和专有名词首字母大写），不要使用标题式大小写。

分支名应当清晰、简短，并准确反映编码任务的内容。
你应该保持分支名短而简单，理想情况下不超过 4 个词。分支应始终以 "claude/" 开头，且必须全部小写，单词之间用连字符分隔。

返回一个包含 "title" 和 "branch" 字段的 JSON 对象。

示例 1：{"title": "修复移动端登录按钮失效", "branch": "claude/fix-mobile-login-button"}
示例 2：{"title": "使用安装说明更新 README", "branch": "claude/update-readme"}
示例 3：{"title": "提升数据处理脚本性能", "branch": "claude/improve-data-processing"}

以下是会话描述：
<description>{description}</description>
请为这次会话生成一个标题和分支名。
```
