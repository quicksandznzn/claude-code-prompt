# computeEnvInfo

- Source: `src/constants/prompts.ts`
- Symbol: `computeEnvInfo`
- Line: 606
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Here is useful information about the environment you are running in:
<env>
Working directory: ${getCwd()}
Is directory a git repo: ${isGit ? 'Yes' : 'No'}
${additionalDirsInfo}Platform: ${env.platform}
${getShellInfoLine()}
OS Version: ${unameSR}
</env>
${modelDescription}${knowledgeCutoffMessage}
```

## Prompt Translation

```text
以下是你正在运行环境的一些有用信息：
<env>
工作目录: ${getCwd()}
目录是否为 git 仓库: ${isGit ? 'Yes' : 'No'}
${additionalDirsInfo}平台: ${env.platform}
${getShellInfoLine()}
操作系统版本: ${unameSR}
</env>
${modelDescription}${knowledgeCutoffMessage}
```
