# BRIEF_TOOL_PROMPT

- Source: `src/tools/BriefTool/prompt.ts`
- Symbol: `BRIEF_TOOL_PROMPT`
- Line: 6
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Send a message the user will read. Text outside this tool is visible in the detail view, but most won't open it — the answer lives here.

`message` supports markdown. `attachments` takes file paths (absolute or cwd-relative) for images, diffs, logs.

`status` labels intent: 'normal' when replying to what they just asked; 'proactive' when you're initiating — a scheduled task finished, a blocker surfaced during background work, you need input on something they haven't asked about. Set it honestly; downstream routing uses it.
```

## Prompt Translation

```text
发送一条用户会阅读的消息。工具外的文本会显示在详情视图中，但大多数人不会打开它——答案就在这里。

`message` 支持 markdown。`attachments` 接受文件路径（绝对路径或相对于当前工作目录的路径），用于图片、diff、日志。

`status` 用来标记意图：当你在回复他们刚刚问的问题时，用 'normal'；当你主动发起时，用 'proactive'——比如计划任务已完成、后台工作中暴露出阻塞，或者你需要就他们还没有问到的事情征求输入。请如实设置；下游路由会使用它。
```
