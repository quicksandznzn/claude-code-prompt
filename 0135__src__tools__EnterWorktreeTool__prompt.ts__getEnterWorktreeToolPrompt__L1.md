# getEnterWorktreeToolPrompt

- Source: `src/tools/EnterWorktreeTool/prompt.ts`
- Symbol: `getEnterWorktreeToolPrompt`
- Line: 1
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Use this tool ONLY when the user explicitly asks to work in a worktree. This tool creates an isolated git worktree and switches the current session into it.

## When to Use

- The user explicitly says "worktree" (e.g., "start a worktree", "work in a worktree", "create a worktree", "use a worktree")

## When NOT to Use

- The user asks to create a branch, switch branches, or work on a different branch — use git commands instead
- The user asks to fix a bug or work on a feature — use normal git workflow unless they specifically mention worktrees
- Never use this tool unless the user explicitly mentions "worktree"

## Requirements

- Must be in a git repository, OR have WorktreeCreate/WorktreeRemove hooks configured in settings.json
- Must not already be in a worktree

## Behavior

- In a git repository: creates a new git worktree inside `.claude/worktrees/` with a new branch based on HEAD
- Outside a git repository: delegates to WorktreeCreate/WorktreeRemove hooks for VCS-agnostic isolation
- Switches the session's working directory to the new worktree
- Use ExitWorktree to leave the worktree mid-session (keep or remove). On session exit, if still in the worktree, the user will be prompted to keep or remove it

## Parameters

- `name` (optional): A name for the worktree. If not provided, a random name is generated.
```

## Prompt Translation

```text
仅在用户明确要求在 worktree 中工作时使用此工具。此工具会创建一个隔离的 git worktree，并将当前会话切换到其中。

## 何时使用

- 用户明确提到“worktree”（例如：“start a worktree”“work in a worktree”“create a worktree”“use a worktree”）

## 何时不使用

- 用户要求创建分支、切换分支，或在其他分支上工作 - 请改用 git 命令
- 用户要求修复 bug 或开发功能 - 除非他们明确提到 worktrees，否则请使用正常的 git 工作流
- 除非用户明确提到“worktree”，否则绝不要使用此工具

## 要求

- 必须位于 git 仓库中，或者在 `settings.json` 中配置了 `WorktreeCreate`/`WorktreeRemove` hooks
- 不能已经处于 worktree 中

## 行为

- 在 git 仓库中：在 `.claude/worktrees/` 内创建一个新的 git worktree，并基于 `HEAD` 新建分支
- 在 git 仓库外：委托给 `WorktreeCreate`/`WorktreeRemove` hooks，以实现与 VCS 无关的隔离
- 将会话的工作目录切换到新的 worktree
- 使用 `ExitWorktree` 在会话中途离开 worktree（保留或移除）。在会话退出时，如果仍处于 worktree 中，系统会提示用户保留还是移除它

## 参数

- `name`（可选）：worktree 的名称。如果未提供，将生成随机名称。
```
