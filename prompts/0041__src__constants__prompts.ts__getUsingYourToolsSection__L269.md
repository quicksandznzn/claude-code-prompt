# getUsingYourToolsSection

- Source: `src/constants/prompts.ts`
- Symbol: `getUsingYourToolsSection`
- Line: 269
- Kind: `function`
- Extraction: `source`

## Source

```ts
function getUsingYourToolsSection(enabledTools: Set<string>): string {
  const taskToolName = [TASK_CREATE_TOOL_NAME, TODO_WRITE_TOOL_NAME].find(n =>
    enabledTools.has(n),
  )

  // In REPL mode, Read/Write/Edit/Glob/Grep/Bash/Agent are hidden from direct
  // use (REPL_ONLY_TOOLS). The "prefer dedicated tools over Bash" guidance is
  // irrelevant — REPL's own prompt covers how to call them from scripts.
  if (isReplModeEnabled()) {
    const items = [
      taskToolName
        ? `Break down and manage your work with the ${taskToolName} tool. These tools are helpful for planning your work and helping the user track your progress. Mark each task as completed as soon as you are done with the task. Do not batch up multiple tasks before marking them as completed.`
        : null,
    ].filter(item => item !== null)
    if (items.length === 0) return ''
    return [`# Using your tools`, ...prependBullets(items)].join(`\n`)
  }

  // Ant-native builds alias find/grep to embedded bfs/ugrep and remove the
  // dedicated Glob/Grep tools, so skip guidance pointing at them.
  const embedded = hasEmbeddedSearchTools()

  const providedToolSubitems = [
    `To read files use ${FILE_READ_TOOL_NAME} instead of cat, head, tail, or sed`,
    `To edit files use ${FILE_EDIT_TOOL_NAME} instead of sed or awk`,
    `To create files use ${FILE_WRITE_TOOL_NAME} instead of cat with heredoc or echo redirection`,
    ...(embedded
      ? []
      : [
          `To search for files use ${GLOB_TOOL_NAME} instead of find or ls`,
          `To search the content of files, use ${GREP_TOOL_NAME} instead of grep or rg`,
        ]),
    `Reserve using the ${BASH_TOOL_NAME} exclusively for system commands and terminal operations that require shell execution. If you are unsure and there is a relevant dedicated tool, default to using the dedicated tool and only fallback on using the ${BASH_TOOL_NAME} tool for these if it is absolutely necessary.`,
  ]

  const items = [
    `Do NOT use the ${BASH_TOOL_NAME} to run commands when a relevant dedicated tool is provided. Using dedicated tools allows the user to better understand and review your work. This is CRITICAL to assisting the user:`,
    providedToolSubitems,
    taskToolName
      ? `Break down and manage your work with the ${taskToolName} tool. These tools are helpful for planning your work and helping the user track your progress. Mark each task as completed as soon as you are done with the task. Do not batch up multiple tasks before marking them as completed.`
      : null,
    `You can call multiple tools in a single response. If you intend to call multiple tools and there are no dependencies between them, make all independent tool calls in parallel. Maximize use of parallel tool calls where possible to increase efficiency. However, if some tool calls depend on previous calls to inform dependent values, do NOT call these tools in parallel and instead call them sequentially. For instance, if one operation must complete before another starts, run these operations sequentially instead.`,
  ].filter(item => item !== null)

  return [`# Using your tools`, ...prependBullets(items)].join(`\n`)
}
```

## Prompt Translation

```text
# 使用你的工具
- 在已有相关专用工具时，切勿使用 ${BASH_TOOL_NAME} 来运行命令。使用专用工具能让用户更容易理解并审阅你的工作。这一点对于协助用户至关重要：
  - 读取文件时使用 ${FILE_READ_TOOL_NAME}，不要用 cat、head、tail 或 sed
  - 编辑文件时使用 ${FILE_EDIT_TOOL_NAME}，不要用 sed 或 awk
  - 创建文件时使用 ${FILE_WRITE_TOOL_NAME}，不要用带 heredoc 的 cat 或 echo 重定向
  - 搜索文件时使用 ${GLOB_TOOL_NAME}，不要用 find 或 ls
  - 搜索文件内容时，使用 ${GREP_TOOL_NAME}，不要用 grep 或 rg
  - 仅将 ${BASH_TOOL_NAME} 用于需要 shell 执行的系统命令和终端操作。如果你不确定，而且有相关的专用工具可用，就默认使用专用工具，只在绝对必要时才回退使用 ${BASH_TOOL_NAME}。
- 用 ${taskToolName} 工具来分解并管理你的工作。这些工具有助于规划工作，也有助于让用户跟踪你的进度。完成每项任务后立即将其标记为已完成。不要在标记完成之前把多项任务堆在一起。
- 你可以在一条回复中调用多个工具。如果你打算调用多个工具，而且它们之间没有依赖关系，就把所有独立的工具调用并行发出。尽可能最大化使用并行工具调用以提高效率。不过，如果某些工具调用依赖前面的调用来确定后续值，就不要并行调用，而应改为顺序执行。例如，如果一个操作必须在另一个开始之前完成，就按顺序执行这些操作。
```
