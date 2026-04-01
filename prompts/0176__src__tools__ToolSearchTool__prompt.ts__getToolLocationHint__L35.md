# getToolLocationHint

- Source: `src/tools/ToolSearchTool/prompt.ts`
- Symbol: `getToolLocationHint`
- Line: 35
- Kind: `function`
- Extraction: `source`

## Source

```ts
function getToolLocationHint(): string {
  const deltaEnabled =
    process.env.USER_TYPE === 'ant' ||
    getFeatureValue_CACHED_MAY_BE_STALE('tengu_glacier_2xr', false)
  return deltaEnabled
    ? 'Deferred tools appear by name in <system-reminder> messages.'
    : 'Deferred tools appear by name in <available-deferred-tools> messages.'
}
```

## Prompt Translation

```text
延迟工具会在 `<system-reminder>` 消息中以名称出现。
延迟工具会在 `<available-deferred-tools>` 消息中以名称出现。
```
