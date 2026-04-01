# getPromptContent

- Source: `src/commands/commit.ts`
- Symbol: `getPromptContent`
- Line: 12
- Kind: `function`
- Extraction: `text`

## Prompt

```text
${prefix}## Context

- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10`

## Git Safety Protocol

- NEVER update the git config
- NEVER skip hooks (--no-verify, --no-gpg-sign, etc) unless the user explicitly requests it
- CRITICAL: ALWAYS create NEW commits. NEVER use git commit --amend, unless the user explicitly requests it
- Do not commit files that likely contain secrets (.env, credentials.json, etc). Warn the user if they specifically request to commit those files
- If there are no changes to commit (i.e., no untracked files and no modifications), do not create an empty commit
- Never use git commands with the -i flag (like git rebase -i or git add -i) since they require interactive input which is not supported

## Your task

Based on the above changes, create a single git commit:

1. Analyze all staged changes and draft a commit message:
   - Look at the recent commits above to follow this repository's commit message style
   - Summarize the nature of the changes (new feature, enhancement, bug fix, refactoring, test, docs, etc.)
   - Ensure the message accurately reflects the changes and their purpose (i.e. "add" means a wholly new feature, "update" means an enhancement to an existing feature, "fix" means a bug fix, etc.)
   - Draft a concise (1-2 sentences) commit message that focuses on the "why" rather than the "what"

2. Stage relevant files and create the commit using HEREDOC syntax:
```

## Prompt Translation

```text
${prefix}## 背景

- 当前 git 状态：!`git status`
- 当前 git diff（已暂存和未暂存的变更）：!`git diff HEAD`
- 当前分支：!`git branch --show-current`
- 最近的提交：!`git log --oneline -10`

## Git 安全协议

- 绝不要更新 git config
- 除非用户明确要求，否则绝不要跳过 hooks（--no-verify、--no-gpg-sign 等）
- 关键：始终创建新的提交。除非用户明确要求，否则绝不要使用 git commit --amend
- 不要提交可能包含密钥的文件（.env、credentials.json 等）。如果用户明确要求提交这些文件，要警告用户
- 如果没有可提交的变更（即没有未跟踪文件，也没有修改），不要创建空提交
- 不要使用带 `-i` 标志的 git 命令（如 git rebase -i 或 git add -i），因为它们需要当前不受支持的交互式输入

## 你的任务

根据上述变更，创建一个单独的 git 提交：

1. 分析所有已暂存的变更并起草提交信息：
   - 查看上面的最近提交，以遵循该仓库的提交信息风格
   - 概括这些变更的性质（新功能、增强、缺陷修复、重构、测试、文档等）
   - 确保信息准确反映变更及其目的（即 "add" 表示全新的功能，"update" 表示对现有功能的增强，"fix" 表示修复缺陷，等等）
   - 起草一条简洁的提交信息（1-2 句），重点说明“为什么”，而不是“做了什么”

2. 暂存相关文件，并使用 HEREDOC 语法创建提交：
```
git commit -m "$(cat <<'EOF'
Commit message here.${commitAttribution ? `\n\n${commitAttribution}` : ''}
EOF
)"
```

You have the capability to call multiple tools in a single response. Stage and create the commit using a single message. Do not use any other tools or do anything else. Do not send any other text or messages besides these tool calls.
```
