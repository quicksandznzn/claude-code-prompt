# getExitWorktreeToolPrompt

- Source: `src/tools/ExitWorktreeTool/prompt.ts`
- Symbol: `getExitWorktreeToolPrompt`
- Line: 1
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Exit a worktree session created by EnterWorktree and return the session to the original working directory.

## Scope

This tool ONLY operates on worktrees created by EnterWorktree in this session. It will NOT touch:
- Worktrees you created manually with `git worktree add`
- Worktrees from a previous session (even if created by EnterWorktree then)
- The directory you're in if EnterWorktree was never called

If called outside an EnterWorktree session, the tool is a **no-op**: it reports that no worktree session is active and takes no action. Filesystem state is unchanged.

## When to Use

- The user explicitly asks to "exit the worktree", "leave the worktree", "go back", or otherwise end the worktree session
- Do NOT call this proactively — only when the user asks

## Parameters

- `action` (required): `"keep"` or `"remove"`
  - `"keep"` — leave the worktree directory and branch intact on disk. Use this if the user wants to come back to the work later, or if there are changes to preserve.
  - `"remove"` — delete the worktree directory and its branch. Use this for a clean exit when the work is done or abandoned.
- `discard_changes` (optional, default false): only meaningful with `action: "remove"`. If the worktree has uncommitted files or commits not on the original branch, the tool will REFUSE to remove it unless this is set to `true`. If the tool returns an error listing changes, confirm with the user before re-invoking with `discard_changes: true`.

## Behavior

- Restores the session's working directory to where it was before EnterWorktree
- Clears CWD-dependent caches (system prompt sections, memory files, plans directory) so the session state reflects the original directory
- If a tmux session was attached to the worktree: killed on `remove`, left running on `keep` (its name is returned so the user can reattach)
- Once exited, EnterWorktree can be called again to create a fresh worktree
```

## Prompt Translation

```text
退出由 `EnterWorktree` 创建的工作树会话，并将会话返回到原始工作目录。

## 作用范围

此工具只会操作本次会话中由 `EnterWorktree` 创建的工作树。它不会影响：
- 你用 `git worktree add` 手动创建的工作树
- 上一次会话中的工作树（即使当时也是由 `EnterWorktree` 创建的）
- 如果从未调用过 `EnterWorktree`，你当前所在的目录

如果在没有 `EnterWorktree` 会话的情况下调用该工具，它会**不执行任何操作**：报告当前没有活动的工作树会话，并且不采取任何动作。文件系统状态不会改变。

## 何时使用

- 用户明确要求“退出工作树”、“离开工作树”、“返回”或以其他方式结束工作树会话
- 不要主动调用它 - 只在用户要求时调用

## 参数

- `action`（必填）：`"keep"` 或 `"remove"`
  - `"keep"` — 保留磁盘上的工作树目录和分支不变。如果用户之后还想回来继续处理，或者有需要保留的更改，就使用这个选项。
  - `"remove"` — 删除工作树目录及其分支。当工作已完成或被放弃，需要干净退出时使用这个选项。
- `discard_changes`（可选，默认 false）：仅在 `action: "remove"` 时有意义。如果工作树中存在未提交文件，或存在不在原始分支上的提交，工具会拒绝删除，除非将其设为 `true`。如果工具返回列出更改的错误，请先与用户确认，再以 `discard_changes: true` 重新调用。

## 行为

- 将会话的工作目录恢复到 `EnterWorktree` 之前的位置
- 清除依赖当前工作目录的缓存（系统提示词段、记忆文件、计划目录），使会话状态反映原始目录
- 如果有一个 tmux 会话附加在该工作树上：在 `remove` 时将其杀死，在 `keep` 时保持运行（会返回其名称，以便用户重新附加）
- 一旦退出，就可以再次调用 `EnterWorktree` 来创建一个新的工作树
```
