# getPrompt

- Source: `src/tools/PowerShellTool/prompt.ts`
- Symbol: `getPrompt`
- Line: 73
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Executes a given PowerShell command with optional timeout. Working directory persists between commands; shell state (variables, functions) does not.

IMPORTANT: This tool is for terminal operations via PowerShell: git, npm, docker, and PS cmdlets. DO NOT use it for file operations (reading, writing, editing, searching, finding files) - use the specialized tools for this instead.

${getEditionSection(edition)}

Before executing the command, please follow these steps:

1. Directory Verification:
   - If the command will create new directories or files, first use `Get-ChildItem` (or `ls`) to verify the parent directory exists and is the correct location

2. Command Execution:
   - Always quote file paths that contain spaces with double quotes
   - Capture the output of the command.

PowerShell Syntax Notes:
   - Variables use $ prefix: $myVar = "value"
   - Escape character is backtick (`), not backslash
   - Use Verb-Noun cmdlet naming: Get-ChildItem, Set-Location, New-Item, Remove-Item
   - Common aliases: ls (Get-ChildItem), cd (Set-Location), cat (Get-Content), rm (Remove-Item)
   - Pipe operator | works similarly to bash but passes objects, not text
   - Use Select-Object, Where-Object, ForEach-Object for filtering and transformation
   - String interpolation: "Hello $name" or "Hello $($obj.Property)"
   - Registry access uses PSDrive prefixes: `HKLM:\SOFTWARE\...`, `HKCU:\...` — NOT raw `HKEY_LOCAL_MACHINE\...`
   - Environment variables: read with `$env:NAME`, set with `$env:NAME = "value"` (NOT `Set-Variable` or bash `export`)
   - Call native exe with spaces in path via call operator: `& "C:\Program Files\App\app.exe" arg1 arg2`

Interactive and blocking commands (will hang — this tool runs with -NonInteractive):
   - NEVER use `Read-Host`, `Get-Credential`, `Out-GridView`, `$Host.UI.PromptForChoice`, or `pause`
   - Destructive cmdlets (`Remove-Item`, `Stop-Process`, `Clear-Content`, etc.) may prompt for confirmation. Add `-Confirm:$false` when you intend the action to proceed. Use `-Force` for read-only/hidden items.
   - Never use `git rebase -i`, `git add -i`, or other commands that open an interactive editor

Passing multiline strings (commit messages, file content) to native executables:
   - Use a single-quoted here-string so PowerShell does not expand `$` or backticks inside. The closing `'@` MUST be at column 0 (no leading whitespace) on its own line — indenting it is a parse error:
<example>
git commit -m @'
Commit message here.
Second line with $literal dollar signs.
'@
</example>
   - Use `@'...'@` (single-quoted, literal) not `@"..."@` (double-quoted, interpolated) unless you need variable expansion
   - For arguments containing `-`, `@`, or other characters PowerShell parses as operators, use the stop-parsing token: `git log --% --format=%H`

Usage notes:
  - The command argument is required.
  - You can specify an optional timeout in milliseconds (up to ${getMaxTimeoutMs()}ms / ${getMaxTimeoutMs() / 60000} minutes). If not specified, commands will timeout after ${getDefaultTimeoutMs()}ms (${getDefaultTimeoutMs() / 60000} minutes).
  - It is very helpful if you write a clear, concise description of what this command does.
  - If the output exceeds ${getMaxOutputLength()} characters, output will be truncated before being returned to you.
${backgroundNote ? backgroundNote + '\n' : ''}  - Avoid using PowerShell to run commands that have dedicated tools, unless explicitly instructed:
    - File search: Use ${GLOB_TOOL_NAME} (NOT Get-ChildItem -Recurse)
    - Content search: Use ${GREP_TOOL_NAME} (NOT Select-String)
    - Read files: Use ${FILE_READ_TOOL_NAME} (NOT Get-Content)
    - Edit files: Use ${FILE_EDIT_TOOL_NAME}
    - Write files: Use ${FILE_WRITE_TOOL_NAME} (NOT Set-Content/Out-File)
    - Communication: Output text directly (NOT Write-Output/Write-Host)
  - When issuing multiple commands:
    - If the commands are independent and can run in parallel, make multiple ${POWERSHELL_TOOL_NAME} tool calls in a single message.
    - If the commands depend on each other and must run sequentially, chain them in a single ${POWERSHELL_TOOL_NAME} call (see edition-specific chaining syntax above).
    - Use `;` only when you need to run commands sequentially but don't care if earlier commands fail.
    - DO NOT use newlines to separate commands (newlines are ok in quoted strings and here-strings)
  - Do NOT prefix commands with `cd` or `Set-Location` -- the working directory is already set to the correct project directory automatically.
${sleepGuidance ? sleepGuidance + '\n' : ''}  - For git commands:
    - Prefer to create a new commit rather than amending an existing commit.
    - Before running destructive operations (e.g., git reset --hard, git push --force, git checkout --), consider whether there is a safer alternative that achieves the same goal. Only use destructive operations when they are truly the best approach.
    - Never skip hooks (--no-verify) or bypass signing (--no-gpg-sign, -c commit.gpgsign=false) unless the user has explicitly asked for it. If a hook fails, investigate and fix the underlying issue.
```

## Prompt Translation

```text
执行给定的 PowerShell 命令，可选设置超时。工作目录会在命令之间保留；shell 状态（变量、函数）不会保留。

重要：此工具用于通过 PowerShell 进行终端操作：git、npm、docker 以及 PowerShell cmdlet。不要将它用于文件操作（读取、写入、编辑、搜索、查找文件）- 这类操作请改用专门工具。

${getEditionSection(edition)}

在执行命令之前，请遵循以下步骤：

1. 目录验证：
   - 如果命令会创建新的目录或文件，先使用 `Get-ChildItem`（或 `ls`）验证父目录存在且位置正确

2. 命令执行：
   - 始终用双引号将包含空格的文件路径括起来
   - 捕获命令输出。

PowerShell 语法说明：
   - 变量使用 `$` 前缀：`$myVar = "value"`
   - 转义字符是反引号（`），不是反斜杠
   - 使用动词-名词式 cmdlet 命名：`Get-ChildItem`、`Set-Location`、`New-Item`、`Remove-Item`
   - 常见别名：`ls`（`Get-ChildItem`）、`cd`（`Set-Location`）、`cat`（`Get-Content`）、`rm`（`Remove-Item`）
   - 管道操作符 `|` 的工作方式类似 bash，但传递的是对象，不是文本
   - 使用 `Select-Object`、`Where-Object`、`ForEach-Object` 进行筛选和转换
   - 字符串插值：`"Hello $name"` 或 `"Hello $($obj.Property)"`
   - 注册表访问使用 PSDrive 前缀：`HKLM:\SOFTWARE\...`、`HKCU:\...` — 不是原始的 `HKEY_LOCAL_MACHINE\...`
   - 环境变量：用 `$env:NAME` 读取，用 `$env:NAME = "value"` 设置（不是 `Set-Variable` 或 bash `export`）
   - 通过调用运算符执行路径中带空格的原生 exe：`& "C:\Program Files\App\app.exe" arg1 arg2`

交互式和会阻塞的命令（会挂起 —— 此工具以 `-NonInteractive` 运行）：
   - 绝不要使用 `Read-Host`、`Get-Credential`、`Out-GridView`、`$Host.UI.PromptForChoice` 或 `pause`
   - 破坏性 cmdlet（`Remove-Item`、`Stop-Process`、`Clear-Content` 等）可能会提示确认。当你打算让操作继续执行时，请添加 `-Confirm:$false`。对只读/隐藏项使用 `-Force`。
   - 绝不要使用 `git rebase -i`、`git add -i` 或其他会打开交互式编辑器的命令

向原生可执行文件传递多行字符串（提交信息、文件内容）：
   - 使用单引号 here-string，这样 PowerShell 不会展开其中的 `$` 或反引号。结束的 `'@` 必须位于第 0 列（前面不能有缩进），并且单独占一行 - 否则会解析错误：
<example>
git commit -m @'
Commit message here.
Second line with $literal dollar signs.
'@
</example>
   - 使用 `@'...'@`（单引号，字面量）而不是 `@"..."@`（双引号，可插值），除非你确实需要变量展开
   - 对于包含 `-`、`@` 或其他 PowerShell 会解析为运算符的字符的参数，请使用停止解析标记：`git log --% --format=%H`

使用说明：
  - 命令参数是必需的。
  - 你可以指定一个可选的毫秒级超时（最多 `${getMaxTimeoutMs()}ms` / `${getMaxTimeoutMs() / 60000}` 分钟）。如果未指定，命令将在 `${getDefaultTimeoutMs()}ms`（`${getDefaultTimeoutMs() / 60000}` 分钟）后超时。
  - 如果你写一段清晰、简洁的说明来描述这个命令的作用，会很有帮助。
  - 如果输出超过 `${getMaxOutputLength()}` 个字符，返回给你之前会先截断输出。
${backgroundNote ? backgroundNote + '\n' : ''}  - 避免使用 PowerShell 去运行已有专用工具的命令，除非明确被指示：
    - 文件搜索：使用 `${GLOB_TOOL_NAME}`（不要用 `Get-ChildItem -Recurse`）
    - 内容搜索：使用 `${GREP_TOOL_NAME}`（不要用 `Select-String`）
    - 读取文件：使用 `${FILE_READ_TOOL_NAME}`（不要用 `Get-Content`）
    - 编辑文件：使用 `${FILE_EDIT_TOOL_NAME}`
    - 写入文件：使用 `${FILE_WRITE_TOOL_NAME}`（不要用 `Set-Content`/`Out-File`）
    - 通信：直接输出文本（不要用 `Write-Output`/`Write-Host`）
  - 当发出多个命令时：
    - 如果这些命令彼此独立并且可以并行运行，请在同一条消息中发起多个 `${POWERSHELL_TOOL_NAME}` 工具调用。
    - 如果这些命令相互依赖并且必须按顺序执行，请将它们串联在一次 `${POWERSHELL_TOOL_NAME}` 调用中（见上方与版本相关的串联语法）。
    - 仅在需要顺序执行命令但不在意前面命令是否失败时，才使用 `;`。
    - 不要用换行分隔命令（换行在引号字符串和 here-string 中可以使用）
  - 不要在命令前加 `cd` 或 `Set-Location` - 工作目录已经自动设置为正确的项目目录。
${sleepGuidance ? sleepGuidance + '\n' : ''}  - 对于 git 命令：
    - 优先创建新的提交，而不是修改已有提交。
    - 在运行破坏性操作之前（例如 `git reset --hard`、`git push --force`、`git checkout --`），请考虑是否有更安全的替代方案可以达成同样目标。只有在这些破坏性操作确实是最佳方案时才使用它们。
    - 除非用户明确要求，否则不要跳过 hooks（`--no-verify`）或绕过签名（`--no-gpg-sign`、`-c commit.gpgsign=false`）。如果 hook 失败，请调查并修复根本问题。
```
