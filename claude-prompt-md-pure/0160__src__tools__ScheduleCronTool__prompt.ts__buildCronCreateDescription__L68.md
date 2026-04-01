# buildCronCreateDescription

- Source: `src/tools/ScheduleCronTool/prompt.ts`
- Symbol: `buildCronCreateDescription`
- Line: 68
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function buildCronCreateDescription(durableEnabled: boolean): string {
  return durableEnabled
    ? 'Schedule a prompt to run at a future time — either recurring on a cron schedule, or once at a specific time. Pass durable: true to persist to .claude/scheduled_tasks.json; otherwise session-only.'
    : 'Schedule a prompt to run at a future time within this Claude session — either recurring on a cron schedule, or once at a specific time.'
}
```

## Prompt Translation

```text
安排一个提示在未来某个时间运行——可以按 cron 计划定期执行，也可以在某个具体时间只执行一次。传入 `durable: true` 可将其持久化到 `.claude/scheduled_tasks.json`；否则仅在会话内有效。
```
