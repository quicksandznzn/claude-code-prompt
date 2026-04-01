# formatCompactSummary

- Source: `src/services/compact/prompt.ts`
- Symbol: `formatCompactSummary`
- Line: 311
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function formatCompactSummary(summary: string): string {
  let formattedSummary = summary

  // Strip analysis section — it's a drafting scratchpad that improves summary
  // quality but has no informational value once the summary is written.
  formattedSummary = formattedSummary.replace(
    /<analysis>[\s\S]*?<\/analysis>/,
    '',
  )

  // Extract and format summary section
  const summaryMatch = formattedSummary.match(/<summary>([\s\S]*?)<\/summary>/)
  if (summaryMatch) {
    const content = summaryMatch[1] || ''
    formattedSummary = formattedSummary.replace(
      /<summary>[\s\S]*?<\/summary>/,
      `Summary:\n${content.trim()}`,
    )
  }

  // Clean up extra whitespace between sections
  formattedSummary = formattedSummary.replace(/\n\n+/g, '\n\n')

  return formattedSummary.trim()
}
```

## Prompt Translation

```text
移除 analysis 部分——它只是一个草稿阶段的临时记录区，虽然能提升摘要质量，但在摘要写好后不再包含任何信息价值。

提取并格式化 summary 部分。

清理各部分之间多余的空白。
```
