# buildCronDeletePrompt

- Source: `src/tools/ScheduleCronTool/prompt.ts`
- Symbol: `buildCronDeletePrompt`
- Line: 124
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function buildCronDeletePrompt(durableEnabled: boolean): string {
  return durableEnabled
    ? `Cancel a cron job previously scheduled with ${CRON_CREATE_TOOL_NAME}. Removes it from .claude/scheduled_tasks.json (durable jobs) or the in-memory session store (session-only jobs).`
    : `Cancel a cron job previously scheduled with ${CRON_CREATE_TOOL_NAME}. Removes it from the in-memory session store.`
}
```

## Prompt Translation

```text
取消先前使用 ${CRON_CREATE_TOOL_NAME} 计划的一个 cron 作业。将其从 .claude/scheduled_tasks.json（持久化作业）或内存中的会话存储（仅会话作业）中移除。
```
