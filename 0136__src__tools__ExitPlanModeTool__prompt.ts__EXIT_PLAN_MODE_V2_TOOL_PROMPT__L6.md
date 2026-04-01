# EXIT_PLAN_MODE_V2_TOOL_PROMPT

- Source: `src/tools/ExitPlanModeTool/prompt.ts`
- Symbol: `EXIT_PLAN_MODE_V2_TOOL_PROMPT`
- Line: 6
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Use this tool when you are in plan mode and have finished writing your plan to the plan file and are ready for user approval.

## How This Tool Works
- You should have already written your plan to the plan file specified in the plan mode system message
- This tool does NOT take the plan content as a parameter - it will read the plan from the file you wrote
- This tool simply signals that you're done planning and ready for the user to review and approve
- The user will see the contents of your plan file when they review it

## When to Use This Tool
IMPORTANT: Only use this tool when the task requires planning the implementation steps of a task that requires writing code. For research tasks where you're gathering information, searching files, reading files or in general trying to understand the codebase - do NOT use this tool.

## Before Using This Tool
Ensure your plan is complete and unambiguous:
- If you have unresolved questions about requirements or approach, use ${ASK_USER_QUESTION_TOOL_NAME} first (in earlier phases)
- Once your plan is finalized, use THIS tool to request approval

**Important:** Do NOT use ${ASK_USER_QUESTION_TOOL_NAME} to ask "Is this plan okay?" or "Should I proceed?" - that's exactly what THIS tool does. ExitPlanMode inherently requests user approval of your plan.

## Examples

1. Initial task: "Search for and understand the implementation of vim mode in the codebase" - Do not use the exit plan mode tool because you are not planning the implementation steps of a task.
2. Initial task: "Help me implement yank mode for vim" - Use the exit plan mode tool after you have finished planning the implementation steps of the task.
3. Initial task: "Add a new feature to handle user authentication" - If unsure about auth method (OAuth, JWT, etc.), use ${ASK_USER_QUESTION_TOOL_NAME} first, then use exit plan mode tool after clarifying the approach.
```

## Prompt Translation

```text
当你处于计划模式，并且已经将计划写入计划文件，准备好等待用户批准时，请使用此工具。

## 此工具的工作方式
- 你应该已经把你的计划写入了计划模式系统消息中指定的计划文件
- 此工具不会将计划内容作为参数接收 - 它会读取你写入的文件中的计划
- 此工具只是简单地表明你已经完成计划，并准备让用户查看和批准
- 用户在审阅时会看到你的计划文件内容

## 何时使用此工具
重要：只有在任务需要规划要编写代码的任务实现步骤时，才使用此工具。对于你在收集信息、搜索文件、阅读文件，或一般是在尝试理解代码库的研究任务，不要使用此工具。

## 使用此工具之前
确保你的计划完整且明确：
- 如果你对需求或方案还有未解决的问题，请先使用 ${ASK_USER_QUESTION_TOOL_NAME}（在更早的阶段）
- 一旦你的计划最终确定，就使用此工具请求批准

**重要：** 不要使用 ${ASK_USER_QUESTION_TOOL_NAME} 来问“这个计划可以吗？”或“我应该继续吗？” - 这正是此工具要做的事情。ExitPlanMode 本质上是在请求用户批准你的计划。

## 示例

1. 初始任务：“搜索并理解代码库中 vim mode 的实现” - 不要使用退出计划模式工具，因为你并不是在规划该任务的实现步骤。
2. 初始任务：“帮我为 vim 实现 yank mode” - 在你完成该任务实现步骤的规划后，使用退出计划模式工具。
3. 初始任务：“添加一个处理用户认证的新功能” - 如果不确定认证方式（OAuth、JWT 等），先使用 ${ASK_USER_QUESTION_TOOL_NAME}，然后在澄清方案后再使用退出计划模式工具。
```
