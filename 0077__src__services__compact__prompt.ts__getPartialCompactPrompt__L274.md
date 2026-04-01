# getPartialCompactPrompt

- Source: `src/services/compact/prompt.ts`
- Symbol: `getPartialCompactPrompt`
- Line: 274
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function getPartialCompactPrompt(
  customInstructions?: string,
  direction: PartialCompactDirection = 'from',
): string {
  const template =
    direction === 'up_to'
      ? PARTIAL_COMPACT_UP_TO_PROMPT
      : PARTIAL_COMPACT_PROMPT
  let prompt = NO_TOOLS_PREAMBLE + template

  if (customInstructions && customInstructions.trim() !== '') {
    prompt += `\n\nAdditional Instructions:\n${customInstructions}`
  }

  prompt += NO_TOOLS_TRAILER

  return prompt
}
```

## Prompt Translation

```text
附加说明：
${customInstructions}
```
