# getPrompt

- Source: `src/tools/TaskCreateTool/prompt.ts`
- Symbol: `getPrompt`
- Line: 5
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Use this tool to create a structured task list for your current coding session. This helps you track progress, organize complex tasks, and demonstrate thoroughness to the user.
It also helps the user understand the progress of the task and overall progress of their requests.

## When to Use This Tool

Use this tool proactively in these scenarios:

- Complex multi-step tasks - When a task requires 3 or more distinct steps or actions
- Non-trivial and complex tasks - Tasks that require careful planning or multiple operations${teammateContext}
- Plan mode - When using plan mode, create a task list to track the work
- User explicitly requests todo list - When the user directly asks you to use the todo list
- User provides multiple tasks - When users provide a list of things to be done (numbered or comma-separated)
- After receiving new instructions - Immediately capture user requirements as tasks
- When you start working on a task - Mark it as in_progress BEFORE beginning work
- After completing a task - Mark it as completed and add any new follow-up tasks discovered during implementation

## When NOT to Use This Tool

Skip using this tool when:
- There is only a single, straightforward task
- The task is trivial and tracking it provides no organizational benefit
- The task can be completed in less than 3 trivial steps
- The task is purely conversational or informational

NOTE that you should not use this tool if there is only one trivial task to do. In this case you are better off just doing the task directly.

## Task Fields

- **subject**: A brief, actionable title in imperative form (e.g., "Fix authentication bug in login flow")
- **description**: What needs to be done
- **activeForm** (optional): Present continuous form shown in the spinner when the task is in_progress (e.g., "Fixing authentication bug"). If omitted, the spinner shows the subject instead.

All tasks are created with status `pending`.

## Tips

- Create tasks with clear, specific subjects that describe the outcome
- After creating tasks, use TaskUpdate to set up dependencies (blocks/blockedBy) if needed
${teammateTips}- Check TaskList first to avoid creating duplicate tasks
```

## Prompt Translation

```text
使用此工具为你当前的编码会话创建一份结构化任务列表。这有助于你跟踪进度、组织复杂任务，并向用户展示你的工作足够周全。
它也有助于用户了解任务的进展以及其请求的整体进展。

## 何时使用此工具

在以下场景中主动使用此工具：

- 复杂的多步骤任务 - 当一个任务需要 3 个或更多不同步骤或操作时
- 非平凡且复杂的任务 - 需要仔细规划或多次操作的任务${teammateContext}
- 计划模式 - 在使用计划模式时，创建任务列表来跟踪工作
- 用户明确请求待办列表 - 当用户直接要求你使用待办列表时
- 用户提供多个任务 - 当用户给出一串待办事项（编号列表或逗号分隔）时
- 收到新指令后 - 立即将用户需求记录为任务
- 开始处理任务时 - 在开始工作之前先将其标记为 in_progress
- 完成任务后 - 将其标记为 completed，并添加在实现过程中发现的任何新的后续任务

## 何时不要使用此工具

在以下情况下跳过使用此工具：
- 只有一个简单直接的任务
- 任务很琐碎，跟踪它没有任何组织上的收益
- 该任务可以在少于 3 个简单步骤内完成
- 该任务纯粹是对话性的或信息性的

请注意，如果只有一个琐碎任务要做，则不应使用此工具。在这种情况下，直接完成任务会更好。

## 任务字段

- **subject**: 一个简短、可执行、采用祈使语气的标题（例如，“修复登录流程中的身份验证错误”）
- **description**: 需要完成的内容
- **activeForm** (optional): 当任务处于 in_progress 时显示在加载指示器中的现在进行时形式（例如，“正在修复身份验证错误”）。如果省略，加载指示器会显示 subject 本身。

所有任务创建时的状态都是 `pending`。

## 提示

- 创建任务时使用清晰、具体的 subject，描述最终结果
- 创建任务后，如有需要，使用 TaskUpdate 设置依赖关系（blocks/blockedBy）
${teammateTips}- 先检查 TaskList，避免创建重复任务
```
