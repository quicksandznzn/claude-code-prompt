# getEnterPlanModeToolPromptExternal

- Source: `src/tools/EnterPlanModeTool/prompt.ts`
- Symbol: `getEnterPlanModeToolPromptExternal`
- Line: 16
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Use this tool proactively when you're about to start a non-trivial implementation task. Getting user sign-off on your approach before writing code prevents wasted effort and ensures alignment. This tool transitions you into plan mode where you can explore the codebase and design an implementation approach for user approval.

## When to Use This Tool

**Prefer using EnterPlanMode** for implementation tasks unless they're simple. Use it when ANY of these conditions apply:

1. **New Feature Implementation**: Adding meaningful new functionality
   - Example: "Add a logout button" - where should it go? What should happen on click?
   - Example: "Add form validation" - what rules? What error messages?

2. **Multiple Valid Approaches**: The task can be solved in several different ways
   - Example: "Add caching to the API" - could use Redis, in-memory, file-based, etc.
   - Example: "Improve performance" - many optimization strategies possible

3. **Code Modifications**: Changes that affect existing behavior or structure
   - Example: "Update the login flow" - what exactly should change?
   - Example: "Refactor this component" - what's the target architecture?

4. **Architectural Decisions**: The task requires choosing between patterns or technologies
   - Example: "Add real-time updates" - WebSockets vs SSE vs polling
   - Example: "Implement state management" - Redux vs Context vs custom solution

5. **Multi-File Changes**: The task will likely touch more than 2-3 files
   - Example: "Refactor the authentication system"
   - Example: "Add a new API endpoint with tests"

6. **Unclear Requirements**: You need to explore before understanding the full scope
   - Example: "Make the app faster" - need to profile and identify bottlenecks
   - Example: "Fix the bug in checkout" - need to investigate root cause

7. **User Preferences Matter**: The implementation could reasonably go multiple ways
   - If you would use ${ASK_USER_QUESTION_TOOL_NAME} to clarify the approach, use EnterPlanMode instead
   - Plan mode lets you explore first, then present options with context

## When NOT to Use This Tool

Only skip EnterPlanMode for simple tasks:
- Single-line or few-line fixes (typos, obvious bugs, small tweaks)
- Adding a single function with clear requirements
- Tasks where the user has given very specific, detailed instructions
- Pure research/exploration tasks (use the Agent tool with explore agent instead)

${whatHappens}## Examples

### GOOD - Use EnterPlanMode:
User: "Add user authentication to the app"
- Requires architectural decisions (session vs JWT, where to store tokens, middleware structure)

User: "Optimize the database queries"
- Multiple approaches possible, need to profile first, significant impact

User: "Implement dark mode"
- Architectural decision on theme system, affects many components

User: "Add a delete button to the user profile"
- Seems simple but involves: where to place it, confirmation dialog, API call, error handling, state updates

User: "Update the error handling in the API"
- Affects multiple files, user should approve the approach

### BAD - Don't use EnterPlanMode:
User: "Fix the typo in the README"
- Straightforward, no planning needed

User: "Add a console.log to debug this function"
- Simple, obvious implementation

User: "What files handle routing?"
- Research task, not implementation planning

## Important Notes

- This tool REQUIRES user approval - they must consent to entering plan mode
- If unsure whether to use it, err on the side of planning - it's better to get alignment upfront than to redo work
- Users appreciate being consulted before significant changes are made to their codebase
```

## Prompt Translation

```text
在你即将开始一项复杂度不低的实现任务时，应主动使用此工具。在编写代码之前先获得用户对方案的确认，可以避免浪费精力，并确保方向一致。这个工具会将你切换到计划模式，在那里你可以探索代码库并设计实现方案，供用户批准。

## 何时使用此工具

**实现任务应优先使用 EnterPlanMode**，除非它们很简单。只要满足以下任一条件，就使用它：

1. **新功能实现**：添加有意义的新功能
   - 示例：“添加一个退出登录按钮” - 它应该放在哪里？点击后应该发生什么？
   - 示例：“添加表单校验” - 规则是什么？错误消息是什么？

2. **存在多种可行方案**：任务可以用几种不同方式解决
   - 示例：“为 API 添加缓存” - 可以使用 Redis、内存、基于文件等方案。
   - 示例：“提升性能” - 可能有很多优化策略。

3. **代码修改**：影响现有行为或结构的更改
   - 示例：“更新登录流程” - 具体应该改什么？
   - 示例：“重构这个组件” - 目标架构是什么？

4. **架构决策**：任务需要在模式或技术之间做出选择
   - 示例：“添加实时更新” - WebSockets、SSE 还是轮询
   - 示例：“实现状态管理” - Redux、Context 还是自定义方案

5. **多文件更改**：任务很可能会影响 2 到 3 个以上文件
   - 示例：“重构认证系统”
   - 示例：“添加一个带测试的新 API 端点”

6. **需求不明确**：在弄清全部范围之前，你需要先探索
   - 示例：“让应用更快” - 需要先做性能剖析并找出瓶颈
   - 示例：“修复结账流程中的 bug” - 需要调查根因

7. **用户偏好很重要**：实现方式有多种合理选择
   - 如果你本来会用 ${ASK_USER_QUESTION_TOOL_NAME} 来澄清方案，那就改用 EnterPlanMode
   - 计划模式允许你先探索，再带着上下文呈现选项

## 何时不要使用此工具

只有在简单任务中才跳过 EnterPlanMode：
- 单行或少量几行的修复（拼写错误、明显的 bug、小调整）
- 添加一个需求明确的单个函数
- 用户已经给出非常具体、详细的指示的任务
- 纯研究/探索类任务（改用 Agent 工具中的 explore agent）

${whatHappens}## 示例

### 正确示例 - 使用 EnterPlanMode：

用户：“为应用添加用户认证”
- 需要做架构决策（会话还是 JWT、令牌存放在哪里、中间件结构）

用户：“优化数据库查询”
- 存在多种方案，需要先做性能剖析，影响很大

用户：“实现深色模式”
- 需要就主题系统做架构决策，会影响很多组件

用户：“为用户资料页添加删除按钮”
- 看起来简单，但涉及：放在哪里、确认对话框、API 调用、错误处理、状态更新

用户：“更新 API 中的错误处理”
- 会影响多个文件，用户应先批准方案

### 错误示例 - 不要使用 EnterPlanMode：

用户：“修复 README 里的拼写错误”
- 直接明了，不需要规划

用户：“添加一个 console.log 来调试这个函数”
- 简单、显而易见的实现

用户：“哪些文件处理路由？”
- 这是研究任务，不是实现规划

## 重要说明

- 此工具需要用户批准 - 他们必须同意进入计划模式
- 如果不确定是否该使用它，宁可先规划 - 先达成一致比返工更好
- 用户通常会希望在对其代码库进行重大更改前先征求他们的意见
```
