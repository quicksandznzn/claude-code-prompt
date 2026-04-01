# generateModelSection

- Source: `src/tools/ConfigTool/prompt.ts`
- Symbol: `generateModelSection`
- Line: 79
- Kind: `function`
- Extraction: `source`

## Source

```ts
function generateModelSection(): string {
  try {
    const options = getModelOptions()
    const lines = options.map(o => {
      const value = o.value === null ? 'null/"default"' : `"${o.value}"`
      return `  - ${value}: ${o.descriptionForModel ?? o.description}`
    })
    return `## Model
- model - Override the default model. Available options:
${lines.join('\n')}`
  } catch {
    return `## Model
- model - Override the default model (sonnet, opus, haiku, best, or full model ID)`
  }
}
```

## Prompt Translation

```text
## 模型
- model - 覆盖默认模型。可用选项：
${lines.join('\n')}
```
