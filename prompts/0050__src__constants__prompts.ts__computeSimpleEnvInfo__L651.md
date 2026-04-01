# computeSimpleEnvInfo

- Source: `src/constants/prompts.ts`
- Symbol: `computeSimpleEnvInfo`
- Line: 651
- Kind: `function`
- Extraction: `source`

## Source

```ts
export async function computeSimpleEnvInfo(
  modelId: string,
  additionalWorkingDirectories?: string[],
): Promise<string> {
  const [isGit, unameSR] = await Promise.all([getIsGit(), getUnameSR()])

  // Undercover: strip all model name/ID references. See computeEnvInfo.
  // DCE: inline the USER_TYPE check at each site — do NOT hoist to a const.
  let modelDescription: string | null = null
  if (process.env.USER_TYPE === 'ant' && isUndercover()) {
    // suppress
  } else {
    const marketingName = getMarketingNameForModel(modelId)
    modelDescription = marketingName
      ? `You are powered by the model named ${marketingName}. The exact model ID is ${modelId}.`
      : `You are powered by the model ${modelId}.`
  }

  const cutoff = getKnowledgeCutoff(modelId)
  const knowledgeCutoffMessage = cutoff
    ? `Assistant knowledge cutoff is ${cutoff}.`
    : null

  const cwd = getCwd()
  const isWorktree = getCurrentWorktreeSession() !== null

  const envItems = [
    `Primary working directory: ${cwd}`,
    isWorktree
      ? `This is a git worktree — an isolated copy of the repository. Run all commands from this directory. Do NOT \`cd\` to the original repository root.`
      : null,
    [`Is a git repository: ${isGit}`],
    additionalWorkingDirectories && additionalWorkingDirectories.length > 0
      ? `Additional working directories:`
      : null,
    additionalWorkingDirectories && additionalWorkingDirectories.length > 0
      ? additionalWorkingDirectories
      : null,
    `Platform: ${env.platform}`,
    getShellInfoLine(),
    `OS Version: ${unameSR}`,
    modelDescription,
    knowledgeCutoffMessage,
    process.env.USER_TYPE === 'ant' && isUndercover()
      ? null
      : `The most recent Claude model family is Claude 4.5/4.6. Model IDs — Opus 4.6: '${CLAUDE_4_5_OR_4_6_MODEL_IDS.opus}', Sonnet 4.6: '${CLAUDE_4_5_OR_4_6_MODEL_IDS.sonnet}', Haiku 4.5: '${CLAUDE_4_5_OR_4_6_MODEL_IDS.haiku}'. When building AI applications, default to the latest and most capable Claude models.`,
    process.env.USER_TYPE === 'ant' && isUndercover()
      ? null
      : `Claude Code is available as a CLI in the terminal, desktop app (Mac/Windows), web app (claude.ai/code), and IDE extensions (VS Code, JetBrains).`,
    process.env.USER_TYPE === 'ant' && isUndercover()
      ? null
      : `Fast mode for Claude Code uses the same ${FRONTIER_MODEL_NAME} model with faster output. It does NOT switch to a different model. It can be toggled with /fast.`,
  ].filter(item => item !== null)

  return [
    `# Environment`,
    `You have been invoked in the following environment: `,
    ...prependBullets(envItems),
  ].join(`\n`)
}
```

## Prompt Translation

```text
# 环境
以下是你所处的环境：
 - 主要工作目录：${cwd}
 - 这是一个 git worktree，即仓库的隔离副本。请从此目录运行所有命令。不要 `cd` 到原始仓库根目录。
  - 是否为 git 仓库：${isGit}
 - 附加工作目录：
 - 平台：${env.platform}
 - Shell：${shellName}
 - 操作系统版本：${unameSR}
 - 你正在使用名为 ${marketingName} 的模型。其准确的模型 ID 是 ${modelId}。
 - 助手的知识截止日期是 ${cutoff}。
 - 最新的 Claude 模型家族是 Claude 4.5/4.6。模型 ID：Opus 4.6: '${CLAUDE_4_5_OR_4_6_MODEL_IDS.opus}', Sonnet 4.6: '${CLAUDE_4_5_OR_4_6_MODEL_IDS.sonnet}', Haiku 4.5: '${CLAUDE_4_5_OR_4_6_MODEL_IDS.haiku}'。在构建 AI 应用时，默认使用最新且能力最强的 Claude 模型。
 - Claude Code 可在终端中以 CLI 形式使用，也可通过桌面应用（Mac/Windows）、网页应用（claude.ai/code）以及 IDE 扩展（VS Code、JetBrains）使用。
 - Claude Code 的快速模式使用相同的 ${FRONTIER_MODEL_NAME} 模型，只是输出更快。它不会切换到其他模型。可通过 /fast 切换。
```
