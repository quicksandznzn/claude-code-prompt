# getSleepGuidance

- Source: `src/tools/PowerShellTool/prompt.ts`
- Symbol: `getSleepGuidance`
- Line: 33
- Kind: `function`
- Extraction: `text`

## Prompt

```text
  - Avoid unnecessary `Start-Sleep` commands:
    - Do not sleep between commands that can run immediately — just run them.
    - If your command is long running and you would like to be notified when it finishes — simply run your command using `run_in_background`. There is no need to sleep in this case.
    - Do not retry failing commands in a sleep loop — diagnose the root cause or consider an alternative approach.
    - If waiting for a background task you started with `run_in_background`, you will be notified when it completes — do not poll.
    - If you must poll an external process, use a check command rather than sleeping first.
    - If you must sleep, keep the duration short (1-5 seconds) to avoid blocking the user.
```

## Prompt Translation

```text
  - 避免不必要的 `Start-Sleep` 命令：
    - 不要在可以立即运行的命令之间睡眠——直接运行它们。
    - 如果你的命令运行时间很长，并且你希望在它完成时收到通知——直接使用 `run_in_background` 运行该命令。在这种情况下不需要睡眠。
    - 不要在睡眠循环里重试失败的命令——先诊断根本原因，或者考虑其他方法。
    - 如果你在等待自己用 `run_in_background` 启动的后台任务，它完成时你会收到通知——不要轮询。
    - 如果必须轮询外部进程，请使用检查命令，而不是先睡眠。
    - 如果必须睡眠，请将持续时间保持得很短（1-5 秒），以免阻塞用户。
```
