# getPrompt

- Source: `src/tools/TeamDeleteTool/prompt.ts`
- Symbol: `getPrompt`
- Line: 1
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function getPrompt(): string {
  return `
# TeamDelete

Remove team and task directories when the swarm work is complete.

This operation:
- Removes the team directory (\`~/.claude/teams/{team-name}/\`)
- Removes the task directory (\`~/.claude/tasks/{team-name}/\`)
- Clears team context from the current session

**IMPORTANT**: TeamDelete will fail if the team still has active members. Gracefully terminate teammates first, then call TeamDelete after all teammates have shut down.

Use this when all teammates have finished their work and you want to clean up the team resources. The team name is automatically determined from the current session's team context.
`.trim()
}
```

## Prompt Translation

```text
# TeamDelete

在群体协作工作完成后，移除团队和任务目录。

此操作会：
- 移除团队目录（`~/.claude/teams/{team-name}/`）
- 移除任务目录（`~/.claude/tasks/{team-name}/`）
- 清除当前会话中的团队上下文

**重要**：如果该团队仍有活跃成员，TeamDelete 将失败。请先优雅地终止队友，然后在所有队友都已关闭后再调用 TeamDelete。

当所有队友都完成工作并且你想清理团队资源时使用此操作。团队名称会根据当前会话中的团队上下文自动确定。
```
