# getPromptContent

- Source: `src/commands/commit-push-pr.ts`
- Symbol: `getPromptContent`
- Line: 26
- Kind: `function`
- Extraction: `text`

## Prompt

```text
${prefix}## Context

- `SAFEUSER`: ${safeUser}
- `whoami`: ${username}
- `git status`: !`git status`
- `git diff HEAD`: !`git diff HEAD`
- `git branch --show-current`: !`git branch --show-current`
- `git diff ${defaultBranch}...HEAD`: !`git diff ${defaultBranch}...HEAD`
- `gh pr view --json number 2>/dev/null || true`: !`gh pr view --json number 2>/dev/null || true`

## Git Safety Protocol

- NEVER update the git config
- NEVER run destructive/irreversible git commands (like push --force, hard reset, etc) unless the user explicitly requests them
- NEVER skip hooks (--no-verify, --no-gpg-sign, etc) unless the user explicitly requests it
- NEVER run force push to main/master, warn the user if they request it
- Do not commit files that likely contain secrets (.env, credentials.json, etc)
- Never use git commands with the -i flag (like git rebase -i or git add -i) since they require interactive input which is not supported

## Your task

Analyze all changes that will be included in the pull request, making sure to look at all relevant commits (NOT just the latest commit, but ALL commits that will be included in the pull request from the git diff ${defaultBranch}...HEAD output above).

Based on the above changes:
1. Create a new branch if on ${defaultBranch} (use SAFEUSER from context above for the branch name prefix, falling back to whoami if SAFEUSER is empty, e.g., `username/feature-name`)
2. Create a single commit with an appropriate message using heredoc syntax${commitAttribution ? `, ending with the attribution text shown in the example below` : ''}:
```

## Prompt Translation

```text
${prefix}## 背景

- `SAFEUSER`: ${safeUser}
- `whoami`: ${username}
- `git status`: !`git status`
- `git diff HEAD`: !`git diff HEAD`
- `git branch --show-current`: !`git branch --show-current`
- `git diff ${defaultBranch}...HEAD`: !`git diff ${defaultBranch}...HEAD`
- `gh pr view --json number 2>/dev/null || true`: !`gh pr view --json number 2>/dev/null || true`

## Git 安全协议

- 绝不要更新 git config
- 除非用户明确要求，否则绝不要运行破坏性/不可逆的 git 命令（如 push --force、hard reset 等）
- 除非用户明确要求，否则绝不要跳过 hooks（--no-verify、--no-gpg-sign 等）
- 绝不要对 main/master 执行强制推送；如果用户要求这样做，要警告用户
- 不要提交可能包含密钥的文件（.env、credentials.json 等）
- 不要使用带 `-i` 标志的 git 命令（如 git rebase -i 或 git add -i），因为它们需要当前不受支持的交互式输入

## 你的任务

分析将包含在拉取请求中的所有变更，并确保查看所有相关提交（不是只看最新提交，而是查看上方 `git diff ${defaultBranch}...HEAD` 输出中将包含在拉取请求里的全部提交）。

基于上述变更：
1. 如果当前位于 ${defaultBranch}，则创建一个新分支（分支名前缀使用上文上下文中的 SAFEUSER；如果 SAFEUSER 为空，则回退为 whoami，例如 `username/feature-name`）
2. 使用 heredoc 语法创建一个带有合适提交信息的单个提交${commitAttribution ? `, ending with the attribution text shown in the example below` : ''}：
```
git commit -m "$(cat <<'EOF'
Commit message here.${commitAttribution ? `\n\n${commitAttribution}` : ''}
EOF
)"
```
3. Push the branch to origin
4. If a PR already exists for this branch (check the gh pr view output above), update the PR title and body using `gh pr edit` to reflect the current diff${addReviewerArg}. Otherwise, create a pull request using `gh pr create` with heredoc syntax for the body${reviewerArg}.
   - IMPORTANT: Keep PR titles short (under 70 characters). Use the body for details.
```
gh pr create --title "Short, descriptive title" --body "$(cat <<'EOF'
## Summary
<1-3 bullet points>

## Test plan
[Bulleted markdown checklist of TODOs for testing the pull request...]${changelogSection}${effectivePrAttribution ? `\n\n${effectivePrAttribution}` : ''}
EOF
)"
```

You have the capability to call multiple tools in a single response. You MUST do all of the above in a single message.${slackStep}

Return the PR URL when you're done, so the user can see it.
```
