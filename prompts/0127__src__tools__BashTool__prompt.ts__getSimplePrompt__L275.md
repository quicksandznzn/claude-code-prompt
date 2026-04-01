# getSimplePrompt

- Source: `src/tools/BashTool/prompt.ts`
- Symbol: `getSimplePrompt`
- Line: 275
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function getSimplePrompt(): string {
  // Ant-native builds alias find/grep to embedded bfs/ugrep in Claude's shell,
  // so we don't steer away from them (and Glob/Grep tools are removed).
  const embedded = hasEmbeddedSearchTools()

  const toolPreferenceItems = [
    ...(embedded
      ? []
      : [
          `File search: Use ${GLOB_TOOL_NAME} (NOT find or ls)`,
          `Content search: Use ${GREP_TOOL_NAME} (NOT grep or rg)`,
        ]),
    `Read files: Use ${FILE_READ_TOOL_NAME} (NOT cat/head/tail)`,
    `Edit files: Use ${FILE_EDIT_TOOL_NAME} (NOT sed/awk)`,
    `Write files: Use ${FILE_WRITE_TOOL_NAME} (NOT echo >/cat <<EOF)`,
    'Communication: Output text directly (NOT echo/printf)',
  ]

  const avoidCommands = embedded
    ? '`cat`, `head`, `tail`, `sed`, `awk`, or `echo`'
    : '`find`, `grep`, `cat`, `head`, `tail`, `sed`, `awk`, or `echo`'

  const multipleCommandsSubitems = [
    `If the commands are independent and can run in parallel, make multiple ${BASH_TOOL_NAME} tool calls in a single message. Example: if you need to run "git status" and "git diff", send a single message with two ${BASH_TOOL_NAME} tool calls in parallel.`,
    `If the commands depend on each other and must run sequentially, use a single ${BASH_TOOL_NAME} call with '&&' to chain them together.`,
    "Use ';' only when you need to run commands sequentially but don't care if earlier commands fail.",
    'DO NOT use newlines to separate commands (newlines are ok in quoted strings).',
  ]

  const gitSubitems = [
    'Prefer to create a new commit rather than amending an existing commit.',
    'Before running destructive operations (e.g., git reset --hard, git push --force, git checkout --), consider whether there is a safer alternative that achieves the same goal. Only use destructive operations when they are truly the best approach.',
    'Never skip hooks (--no-verify) or bypass signing (--no-gpg-sign, -c commit.gpgsign=false) unless the user has explicitly asked for it. If a hook fails, investigate and fix the underlying issue.',
  ]

  const sleepSubitems = [
    'Do not sleep between commands that can run immediately — just run them.',
    ...(feature('MONITOR_TOOL')
      ? [
          'Use the Monitor tool to stream events from a background process (each stdout line is a notification). For one-shot "wait until done," use Bash with run_in_background instead.',
        ]
      : []),
    'If your command is long running and you would like to be notified when it finishes — use `run_in_background`. No sleep needed.',
    'Do not retry failing commands in a sleep loop — diagnose the root cause.',
    'If waiting for a background task you started with `run_in_background`, you will be notified when it completes — do not poll.',
    ...(feature('MONITOR_TOOL')
      ? [
          '`sleep N` as the first command with N ≥ 2 is blocked. If you need a delay (rate limiting, deliberate pacing), keep it under 2 seconds.',
        ]
      : [
          'If you must poll an external process, use a check command (e.g. `gh run view`) rather than sleeping first.',
          'If you must sleep, keep the duration short (1-5 seconds) to avoid blocking the user.',
        ]),
  ]
  const backgroundNote = getBackgroundUsageNote()

  const instructionItems: Array<string | string[]> = [
    'If your command will create new directories or files, first use this tool to run `ls` to verify the parent directory exists and is the correct location.',
    'Always quote file paths that contain spaces with double quotes in your command (e.g., cd "path with spaces/file.txt")',
    'Try to maintain your current working directory throughout the session by using absolute paths and avoiding usage of `cd`. You may use `cd` if the User explicitly requests it.',
    `You may specify an optional timeout in milliseconds (up to ${getMaxTimeoutMs()}ms / ${getMaxTimeoutMs() / 60000} minutes). By default, your command will timeout after ${getDefaultTimeoutMs()}ms (${getDefaultTimeoutMs() / 60000} minutes).`,
    ...(backgroundNote !== null ? [backgroundNote] : []),
    'When issuing multiple commands:',
    multipleCommandsSubitems,
    'For git commands:',
    gitSubitems,
    'Avoid unnecessary `sleep` commands:',
    sleepSubitems,
    ...(embedded
      ? [
          // bfs (which backs `find`) uses Oniguruma for -regex, which picks the
          // FIRST matching alternative (leftmost-first), unlike GNU find's
          // POSIX leftmost-longest. This silently drops matches when a shorter
          // alternative is a prefix of a longer one.
          "When using `find -regex` with alternation, put the longest alternative first. Example: use `'.*\\.\\(tsx\\|ts\\)'` not `'.*\\.\\(ts\\|tsx\\)'` — the second form silently skips `.tsx` files.",
        ]
      : []),
  ]

  return [
    'Executes a given bash command and returns its output.',
    '',
    "The working directory persists between commands, but shell state does not. The shell environment is initialized from the user's profile (bash or zsh).",
    '',
    `IMPORTANT: Avoid using this tool to run ${avoidCommands} commands, unless explicitly instructed or after you have verified that a dedicated tool cannot accomplish your task. Instead, use the appropriate dedicated tool as this will provide a much better experience for the user:`,
    '',
    ...prependBullets(toolPreferenceItems),
    `While the ${BASH_TOOL_NAME} tool can do similar things, it’s better to use the built-in tools as they provide a better user experience and make it easier to review tool calls and give permission.`,
    '',
    '# Instructions',
    ...prependBullets(instructionItems),
    getSimpleSandboxSection(),
    ...(getCommitAndPRInstructions() ? ['', getCommitAndPRInstructions()] : []),
  ].join('\n')
}
```

## Prompt Translation

```text
执行给定的 bash 命令并返回其输出。

命令之间会保留工作目录，但 shell 状态不会保留。shell 环境会根据用户的配置文件（bash 或 zsh）初始化。

重要：除非被明确要求，或者你已经验证某个专用工具无法完成任务，否则不要使用此工具来运行 `find`、`grep`、`cat`、`head`、`tail`、`sed`、`awk` 或 `echo` 命令。相反，请使用相应的专用工具，因为这会为用户带来更好的体验：

 - 文件搜索：使用 Glob（不要使用 find 或 ls）
 - 内容搜索：使用 Grep（不要使用 grep 或 rg）
 - 读取文件：使用 Read（不要使用 cat/head/tail）
 - 编辑文件：使用 Edit（不要使用 sed/awk）
 - 写入文件：使用 Write（不要使用 echo >/cat <<EOF）
 - 沟通：直接输出文本（不要使用 echo/printf）
虽然 Bash tool 也能做类似的事情，但更建议使用内置工具，因为它们能提供更好的用户体验，也更便于审查工具调用并授予权限。

# 说明
 - 如果你的命令会创建新的目录或文件，先使用此工具运行 `ls`，确认父目录存在且位置正确。
 - 如果命令中的文件路径包含空格，务必用双引号将其括起来（例如，cd "path with spaces/file.txt"）
 - 尽量在整个会话中保持当前工作目录不变，使用绝对路径并避免使用 `cd`。如果用户明确要求，可以使用 `cd`。
 - 你可以指定可选的超时时间（毫秒，最多 600000ms / 10 分钟）。默认情况下，命令会在 120000ms（2 分钟）后超时。
 - 你可以使用 `run_in_background` 参数在后台运行命令。只有在你不需要立刻得到结果，并且可以接受在命令稍后完成时收到通知时才使用它。你不需要马上检查输出 - 命令完成时会通知你。使用此参数时，不需要在命令末尾加 `&`。
 - 当发出多个命令时：
  - 如果这些命令彼此独立且可以并行运行，请在一条消息中发起多个 Bash tool 调用。例如：如果你需要运行 "git status" 和 "git diff"，请发送一条包含两个 Bash tool 并行调用的消息。
  - 如果这些命令彼此依赖且必须顺序执行，请使用一次 Bash 调用，并用 `&&` 将它们串联起来。
  - 只有在你需要顺序执行命令，但不在乎前面的命令是否失败时，才使用 `;`。
  - 不要用换行来分隔命令（但在带引号的字符串里可以使用换行）。
 - 对于 git 命令：
  - 优先创建新提交，而不是修改已有提交。
  - 在执行破坏性操作（例如 `git reset --hard`、`git push --force`、`git checkout --`）之前，先考虑是否有更安全的替代方案能够达到相同目标。只有在它们确实是最佳方案时才使用破坏性操作。
  - 除非用户明确要求，否则不要跳过 hooks（--no-verify）或绕过签名（--no-gpg-sign、-c commit.gpgsign=false）。如果某个 hook 失败，请调查并修复根本问题。
 - 避免不必要的 `sleep` 命令：
  - 对于可以立即执行的命令，不要在它们之间 sleep，直接运行即可。
  - 如果你的命令运行时间较长，并且你希望在它完成时收到通知，请使用 `run_in_background`。无需 sleep。
  - 不要用 sleep 循环重试失败的命令，而应诊断根本原因。
  - 如果你在等待自己通过 `run_in_background` 启动的后台任务，它完成时会通知你 - 不要轮询。
  - 如果你必须轮询外部进程，请使用检查命令（例如 `gh run view`），而不是先 sleep。
  - 如果你必须 sleep，请保持时长很短（1-5 秒），以避免阻塞用户。


# 使用 git 提交更改

只有在用户要求时才创建提交。如果不清楚，先询问。当用户要求你创建新的 git 提交时，请认真遵循以下步骤：

你可以在一次回复中调用多个工具。当用户同时请求多个彼此独立的信息，且所有命令都很可能成功时，为了获得最佳性能，请并行运行多个工具调用。下面的编号步骤说明了哪些命令应并行批处理。

Git 安全协议：
- 绝不要更新 git config
- 绝不要运行破坏性的 git 命令（push --force、reset --hard、checkout .、restore .、clean -f、branch -D），除非用户明确要求这些操作。未经授权进行破坏性操作没有帮助，而且可能导致工作丢失，所以只有在得到直接指示时才应该运行这些命令
- 绝不要跳过 hooks（--no-verify、--no-gpg-sign 等），除非用户明确要求
- 绝不要强制推送到 main/master；如果用户要求这样做，要提醒他们
- 关键：始终创建新的提交，而不是修改已有提交，除非用户明确要求 git amend。当 pre-commit hook 失败时，提交并没有发生 - 因此 --amend 会修改前一个提交，这可能会破坏工作或丢失之前的更改。相反，在 hook 失败后，修复问题、重新暂存，并创建一个新的提交
- 在暂存文件时，优先按文件名添加具体文件，而不是使用 "git add -A" 或 "git add ."，因为这可能会意外包含敏感文件（.env、credentials）或大型二进制文件
- 除非用户明确要求，否则绝不要提交更改。只在明确要求时才提交，这一点非常重要，否则用户会觉得你过于主动

1. 在一个回复中并行运行以下 bash 命令，每个都使用 Bash tool：
  - 运行 git status 命令查看所有未跟踪文件。重要：绝不要使用 -uall 标志，因为它在大型仓库中可能导致内存问题。
  - 运行 git diff 命令查看将要提交的已暂存和未暂存更改。
  - 运行 git log 命令查看最近的提交信息，以便你遵循这个仓库的提交信息风格。
2. 分析所有已暂存的更改（包括之前已暂存和新添加的），并起草一条提交信息：
  - 总结更改的性质（例如：新功能、对现有功能的增强、bug 修复、重构、测试、文档等）。确保信息准确反映更改及其目的（即 "add" 表示全新功能，"update" 表示对现有功能的增强，"fix" 表示 bug 修复，等等）。
  - 不要提交很可能包含秘密信息的文件（.env、credentials.json 等）。如果用户明确要求提交这些文件，要提醒他们
  - 起草一条简洁（1-2 句）的提交信息，重点强调 "为什么" 而不是 "做了什么"
  - 确保它准确反映更改及其目的
3. 在一个回复中并行运行以下命令：
  - 将相关的未跟踪文件添加到暂存区。
  - 使用如下格式创建提交信息的提交：
   Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>
  - 在提交完成后运行 git status 以验证是否成功。
   注意：git status 依赖提交完成，所以应在提交后顺序运行它。
4. 如果提交因为 pre-commit hook 失败：修复问题并创建一个新的提交

重要说明：
- 绝不要运行额外的命令来读取或探索代码，除了 git bash 命令
- 绝不要使用 TodoWrite 或 Agent 工具
- 未经用户明确要求，不要 push 到远程仓库
- 重要：绝不要使用带有 -i 标志的 git 命令（例如 git rebase -i 或 git add -i），因为它们需要交互输入，而这不受支持
- 重要：不要在 git rebase 命令中使用 --no-edit，因为 --no-edit 不是 git rebase 的有效选项
- 如果没有要提交的更改（即没有未跟踪文件和没有修改），不要创建空提交
- 为了确保格式良好，务必通过 HEREDOC 传递提交信息，如下例所示：
<example>
git commit -m "$(cat <<'EOF'
   提交信息写在这里。

   Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>
   EOF
   )"
</example>

# 创建拉取请求
对于所有与 GitHub 相关的任务，包括处理 issue、拉取请求、checks 和 releases，请通过 Bash tool 使用 gh 命令。如果给出的是 GitHub URL，请使用 gh 命令获取所需信息。

重要：当用户要求你创建拉取请求时，请认真遵循以下步骤：

1. 使用 Bash tool 并行运行以下 bash 命令，以便了解当前分支自从从 main 分支分叉以来的状态：
   - 运行 git status 命令查看所有未跟踪文件（绝不要使用 -uall 标志）
   - 运行 git diff 命令查看将要提交的已暂存和未暂存更改
   - 检查当前分支是否跟踪远程分支，以及它是否与远程保持同步，这样你就知道是否需要 push 到远程
   - 运行 git log 命令和 `git diff [base-branch]...HEAD`，以了解当前分支的完整提交历史（从它与基础分支分叉的时刻开始）
2. 分析将包含在拉取请求中的所有更改，确保查看所有相关提交（**不只是最新提交，而是拉取请求中将包含的所有提交！！！**），并起草一个拉取请求标题和摘要：
   - 保持 PR 标题简短（少于 70 个字符）
   - 详细内容写在 description/body 里，不要放在标题里
3. 并行运行以下命令：
   - 如有需要，创建新分支
   - 如有需要，使用 -u 标志 push 到远程
   - 使用下面的格式通过 gh pr create 创建 PR。使用 HEREDOC 传递正文，以确保格式正确。
<example>
gh pr create --title "the pr title" --body "$(cat <<'EOF'
## 概要
<1-3 个要点>

## 测试计划
[用于测试该拉取请求的 Markdown 待办事项项目符号清单...]

🤖 由 [Claude Code](https://claude.com/claude-code) 生成
EOF
)"
</example>

重要：
- 绝不要使用 TodoWrite 或 Agent 工具
- 完成后返回 PR URL，这样用户就能看到它

# 其他常见操作
使用 gh 命令通过 Bash tool 处理所有与 GitHub 相关的任务，包括 issue、pull request、checks 和 releases。如果给出的是 GitHub URL，请使用 gh 命令获取所需信息。
```
