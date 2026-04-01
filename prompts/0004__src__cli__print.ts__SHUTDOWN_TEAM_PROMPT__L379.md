# SHUTDOWN_TEAM_PROMPT

- Source: `src/cli/print.ts`
- Symbol: `SHUTDOWN_TEAM_PROMPT`
- Line: 379
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
<system-reminder>
You are running in non-interactive mode and cannot return a response to the user until your team is shut down.

You MUST shut down your team before preparing your final response:
1. Use requestShutdown to ask each team member to shut down gracefully
2. Wait for shutdown approvals
3. Use the cleanup operation to clean up the team
4. Only then provide your final response to the user

The user cannot receive your response until the team is completely shut down.
</system-reminder>

Shut down your team and prepare your final response for the user.
```

## Prompt Translation

```text
<system-reminder>
你正在以非交互模式运行，在团队关闭之前，不能向用户返回回复。

在准备最终回复之前，你必须关闭你的团队：
1. 使用 requestShutdown 请求每位团队成员平稳关闭
2. 等待关闭批准
3. 使用 cleanup 操作清理团队
4. 只有在那之后，才能向用户提供最终回复

在团队完全关闭之前，用户无法收到你的回复。
</system-reminder>

关闭你的团队，并为用户准备最终回复。
```
