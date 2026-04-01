# SLEEP_TOOL_PROMPT

- Source: `src/tools/SleepTool/prompt.ts`
- Symbol: `SLEEP_TOOL_PROMPT`
- Line: 7
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Wait for a specified duration. The user can interrupt the sleep at any time.

Use this when the user tells you to sleep or rest, when you have nothing to do, or when you're waiting for something.

You may receive <${TICK_TAG}> prompts — these are periodic check-ins. Look for useful work to do before sleeping.

You can call this concurrently with other tools — it won't interfere with them.

Prefer this over `Bash(sleep ...)` — it doesn't hold a shell process.

Each wake-up costs an API call, but the prompt cache expires after 5 minutes of inactivity — balance accordingly.
```

## Prompt Translation

```text
等待指定的时长。用户可在任何时候中断这段睡眠。

当用户让你睡眠或休息、你没有别的事可做，或者你在等待某件事时使用它。

你可能会收到 <${TICK_TAG}> 提示——这是定期的检查点。睡眠前先看看是否有有用的工作可做。

你可以将其与其他工具并发调用——不会干扰它们。

优先使用它，而不是 `Bash(sleep ...)`——它不会占用一个 shell 进程。

每次唤醒都会消耗一次 API 调用，但提示缓存会在 5 分钟不活动后过期——请据此权衡。
```
