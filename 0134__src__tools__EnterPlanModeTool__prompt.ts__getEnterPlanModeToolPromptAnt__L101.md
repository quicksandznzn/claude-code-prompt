# getEnterPlanModeToolPromptAnt

- Source: `src/tools/EnterPlanModeTool/prompt.ts`
- Symbol: `getEnterPlanModeToolPromptAnt`
- Line: 101
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Use this tool when a task has genuine ambiguity about the right approach and getting user input before coding would prevent significant rework. This tool transitions you into plan mode where you can explore the codebase and design an implementation approach for user approval.

## When to Use This Tool

Plan mode is valuable when the implementation approach is genuinely unclear. Use it when:

1. **Significant Architectural Ambiguity**: Multiple reasonable approaches exist and the choice meaningfully affects the codebase
   - Example: "Add caching to the API" - Redis vs in-memory vs file-based
   - Example: "Add real-time updates" - WebSockets vs SSE vs polling

2. **Unclear Requirements**: You need to explore and clarify before you can make progress
   - Example: "Make the app faster" - need to profile and identify bottlenecks
   - Example: "Refactor this module" - need to understand what the target architecture should be

3. **High-Impact Restructuring**: The task will significantly restructure existing code and getting buy-in first reduces risk
   - Example: "Redesign the authentication system"
   - Example: "Migrate from one state management approach to another"

## When NOT to Use This Tool

Skip plan mode when you can reasonably infer the right approach:
- The task is straightforward even if it touches multiple files
- The user's request is specific enough that the implementation path is clear
- You're adding a feature with an obvious implementation pattern (e.g., adding a button, a new endpoint following existing conventions)
- Bug fixes where the fix is clear once you understand the bug
- Research/exploration tasks (use the Agent tool instead)
- The user says something like "can we work on X" or "let's do X" — just get started

When in doubt, prefer starting work and using ${ASK_USER_QUESTION_TOOL_NAME} for specific questions over entering a full planning phase.

${whatHappens}## Examples

### GOOD - Use EnterPlanMode:
User: "Add user authentication to the app"
- Genuinely ambiguous: session vs JWT, where to store tokens, middleware structure

User: "Redesign the data pipeline"
- Major restructuring where the wrong approach wastes significant effort

### BAD - Don't use EnterPlanMode:
User: "Add a delete button to the user profile"
- Implementation path is clear; just do it

User: "Can we work on the search feature?"
- User wants to get started, not plan

User: "Update the error handling in the API"
- Start working; ask specific questions if needed

User: "Fix the typo in the README"
- Straightforward, no planning needed

## Important Notes

- This tool REQUIRES user approval - they must consent to entering plan mode
```

## Prompt Translation

```text
使用此工具的场景是：任务在正确做法上确实存在歧义，而且在编码前先获取用户输入可以避免大量返工。此工具会将你切换到计划模式，在那里你可以探索代码库并设计实现方案，以供用户批准。

## 何时使用此工具

当实现方案确实不明确时，计划模式很有价值。以下情况使用它：

1. **显著的架构歧义**：存在多个合理方案，而且选择会实质性影响代码库
   - 示例：“为 API 添加缓存” - Redis、内存缓存还是基于文件
   - 示例：“添加实时更新” - WebSocket、SSE 还是轮询

2. **需求不清晰**：你需要先探索并澄清，才能继续推进
   - 示例：“让应用更快” - 需要分析并找出瓶颈
   - 示例：“重构这个模块” - 需要了解目标架构应是什么样子

3. **高影响重构**：任务会显著重组现有代码，先取得认可可以降低风险
   - 示例：“重新设计身份验证系统”
   - 示例：“从一种状态管理方案迁移到另一种”

## 何时不要使用此工具

当你能够合理推断出正确方案时，跳过计划模式：
- 即使会涉及多个文件，任务也很直接
- 用户的请求足够具体，实现路径已经很清晰
- 你要添加的功能有明显的实现模式（例如：添加按钮、按现有约定添加新端点）
- 当你理解 bug 后，修复方法很明确的 bug 修复
- 研究/探索类任务（改用 Agent 工具）
- 用户说类似“我们能做 X 吗”或“我们来做 X 吧”这样的内容时，直接开始即可

拿不准时，比起进入完整的规划阶段，更应先开始工作，并针对具体问题使用 ${ASK_USER_QUESTION_TOOL_NAME}。

${whatHappens}## 示例

### 合适 - 使用 EnterPlanMode:
用户：“为应用添加用户身份验证”
- 确实存在歧义：会话 vs JWT、令牌存放位置、中间件结构

用户：“重新设计数据管道”
- 这属于大规模重构，错误的方案会浪费大量精力

### 不合适 - 不要使用 EnterPlanMode:
用户：“为用户资料页添加删除按钮”
- 实现路径很清晰，直接做即可

用户：“我们能做搜索功能吗？”
- 用户是想开始动手，不是在做规划

用户：“更新 API 中的错误处理”
- 直接开始做；如有需要，再问具体问题

用户：“修复 README 里的拼写错误”
- 很直接，不需要规划

## 重要说明

- 此工具需要用户批准 - 他们必须同意进入计划模式
```
