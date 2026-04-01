# buildCronListPrompt

- Source: `src/tools/ScheduleCronTool/prompt.ts`
- Symbol: `buildCronListPrompt`
- Line: 131
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function buildCronListPrompt(durableEnabled: boolean): string {
  return durableEnabled
    ? `List all cron jobs scheduled via ${CRON_CREATE_TOOL_NAME}, both durable (.claude/scheduled_tasks.json) and session-only.`
    : `List all cron jobs scheduled via ${CRON_CREATE_TOOL_NAME} in this session.`
}
```

## Prompt Translation

```text
列出通过 `${CRON_CREATE_TOOL_NAME}` 调度的所有 cron 作业，包括持久化的（.claude/scheduled_tasks.json）和仅限当前会话的。
列出当前会话中通过 `${CRON_CREATE_TOOL_NAME}` 调度的所有 cron 作业。
```
