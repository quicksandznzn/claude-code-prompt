# generateSectionReminders

- Source: `src/services/SessionMemory/prompts.ts`
- Symbol: `generateSectionReminders`
- Line: 164
- Kind: `function`
- Extraction: `source`

## Source

```ts
function generateSectionReminders(
  sectionSizes: Record<string, number>,
  totalTokens: number,
): string {
  const overBudget = totalTokens > MAX_TOTAL_SESSION_MEMORY_TOKENS
  const oversizedSections = Object.entries(sectionSizes)
    .filter(([_, tokens]) => tokens > MAX_SECTION_LENGTH)
    .sort(([, a], [, b]) => b - a)
    .map(
      ([section, tokens]) =>
        `- "${section}" is ~${tokens} tokens (limit: ${MAX_SECTION_LENGTH})`,
    )

  if (oversizedSections.length === 0 && !overBudget) {
    return ''
  }

  const parts: string[] = []

  if (overBudget) {
    parts.push(
      `\n\nCRITICAL: The session memory file is currently ~${totalTokens} tokens, which exceeds the maximum of ${MAX_TOTAL_SESSION_MEMORY_TOKENS} tokens. You MUST condense the file to fit within this budget. Aggressively shorten oversized sections by removing less important details, merging related items, and summarizing older entries. Prioritize keeping "Current State" and "Errors & Corrections" accurate and detailed.`,
    )
  }

  if (oversizedSections.length > 0) {
    parts.push(
      `\n\n${overBudget ? 'Oversized sections to condense' : 'IMPORTANT: The following sections exceed the per-section limit and MUST be condensed'}:\n${oversizedSections.join('\n')}`,
    )
  }

  return parts.join('')
}
```

## Prompt Translation

```text
紧急：会话记忆文件当前约为 ${totalTokens} 个 token，已超过 ${MAX_TOTAL_SESSION_MEMORY_TOKENS} 个 token 的上限。你必须将文件压缩到这个预算内。通过删除不太重要的细节、合并相关条目、总结较早的记录来尽可能大幅缩短超长部分。优先保持“当前状态”和“错误与修正”的准确且详尽。

重要：以下部分超过了每部分上限，必须压缩：
- "${section}" 约为 ${tokens} 个 token（上限：${MAX_SECTION_LENGTH}）
```
