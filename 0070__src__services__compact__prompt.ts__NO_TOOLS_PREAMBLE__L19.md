# NO_TOOLS_PREAMBLE

- Source: `src/services/compact/prompt.ts`
- Symbol: `NO_TOOLS_PREAMBLE`
- Line: 19
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
CRITICAL: Respond with TEXT ONLY. Do NOT call any tools.

- Do NOT use Read, Bash, Grep, Glob, Edit, Write, or ANY other tool.
- You already have all the context you need in the conversation above.
- Tool calls will be REJECTED and will waste your only turn — you will fail the task.
- Your entire response must be plain text: an <analysis> block followed by a <summary> block.
```

## Prompt Translation

```text
重要：仅用文本响应。不要调用任何工具。

- 不要使用 Read、Bash、Grep、Glob、Edit、Write 或任何其他工具。
- 你已经拥有上文对话中所需的全部上下文。
- 工具调用会被拒绝，并会浪费你唯一的一次机会——你将无法完成任务。
- 你的整个回复必须是纯文本：先是一个 <analysis> 块，然后是一个 <summary> 块。
```
