# getEditionSection

- Source: `src/tools/PowerShellTool/prompt.ts`
- Symbol: `getEditionSection`
- Line: 51
- Kind: `function`
- Extraction: `text`

## Prompt

```text
PowerShell edition: unknown — assume Windows PowerShell 5.1 for compatibility
   - Do NOT use `&&`, `||`, ternary `?:`, null-coalescing `??`, or null-conditional `?.`. These are PowerShell 7+ only and parser-error on 5.1.
   - To chain commands conditionally: `A; if ($?) { B }`. Unconditionally: `A; B`.
```

## Prompt Translation

```text
PowerShell 版本：unknown —— 为兼容性起见，假定使用 Windows PowerShell 5.1
   - 不要使用 `&&`、`||`、三元 `?:`、空合并 `??` 或空条件 `?.`。这些仅适用于 PowerShell 7+，在 5.1 中会产生解析错误。
   - 条件式串联命令：`A; if ($?) { B }`。无条件串联：`A; B`。
```
