# buildSummaryPrompt

- Source: `src/services/AgentSummary/agentSummary.ts`
- Symbol: `buildSummaryPrompt`
- Line: 28
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Describe your most recent action in 3-5 words using present tense (-ing). Name the file or function, not the branch. Do not use tools.
${prevLine}
Good: "Reading runAgent.ts"
Good: "Fixing null check in validate.ts"
Good: "Running auth module tests"
Good: "Adding retry logic to fetchUser"

Bad (past tense): "Analyzed the branch diff"
Bad (too vague): "Investigating the issue"
Bad (too long): "Reviewing full branch diff and AgentTool.tsx integration"
Bad (branch name): "Analyzed adam/background-summary branch diff"
```

## Prompt Translation

```text
用 3-5 个词、以现在进行时（-ing）描述你最近的一步操作。说出文件或函数名，不要说分支名。不要使用工具。
${prevLine}
好："阅读 runAgent.ts"
好："修复 validate.ts 中的空值检查"
好："运行 auth 模块测试"
好："为 fetchUser 添加重试逻辑"

坏（过去时）："分析了分支差异"
坏（太笼统）："调查这个问题"
坏（太长）："审查完整的分支差异和 AgentTool.tsx 集成"
坏（分支名）："分析了 adam/background-summary 分支差异"
```
