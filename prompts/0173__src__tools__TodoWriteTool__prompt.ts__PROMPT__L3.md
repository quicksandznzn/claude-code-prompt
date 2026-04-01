# PROMPT

- Source: `src/tools/TodoWriteTool/prompt.ts`
- Symbol: `PROMPT`
- Line: 3
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Use this tool to create and manage a structured task list for your current coding session. This helps you track progress, organize complex tasks, and demonstrate thoroughness to the user.
It also helps the user understand the progress of the task and overall progress of their requests.

## When to Use This Tool
Use this tool proactively in these scenarios:

1. Complex multi-step tasks - When a task requires 3 or more distinct steps or actions
2. Non-trivial and complex tasks - Tasks that require careful planning or multiple operations
3. User explicitly requests todo list - When the user directly asks you to use the todo list
4. User provides multiple tasks - When users provide a list of things to be done (numbered or comma-separated)
5. After receiving new instructions - Immediately capture user requirements as todos
6. When you start working on a task - Mark it as in_progress BEFORE beginning work. Ideally you should only have one todo as in_progress at a time
7. After completing a task - Mark it as completed and add any new follow-up tasks discovered during implementation

## When NOT to Use This Tool

Skip using this tool when:
1. There is only a single, straightforward task
2. The task is trivial and tracking it provides no organizational benefit
3. The task can be completed in less than 3 trivial steps
4. The task is purely conversational or informational

NOTE that you should not use this tool if there is only one trivial task to do. In this case you are better off just doing the task directly.

## Examples of When to Use the Todo List

<example>
User: I want to add a dark mode toggle to the application settings. Make sure you run the tests and build when you're done!
Assistant: *Creates todo list with the following items:*
1. Creating dark mode toggle component in Settings page
2. Adding dark mode state management (context/store)
3. Implementing CSS-in-JS styles for dark theme
4. Updating existing components to support theme switching
5. Running tests and build process, addressing any failures or errors that occur
*Begins working on the first task*

<reasoning>
The assistant used the todo list because:
1. Adding dark mode is a multi-step feature requiring UI, state management, and styling changes
2. The user explicitly requested tests and build be run afterward
3. The assistant inferred that tests and build need to pass by adding "Ensure tests and build succeed" as the final task
</reasoning>
</example>

<example>
User: Help me rename the function getCwd to getCurrentWorkingDirectory across my project
Assistant: *Uses grep or search tools to locate all instances of getCwd in the codebase*
I've found 15 instances of 'getCwd' across 8 different files.
*Creates todo list with specific items for each file that needs updating*

<reasoning>
The assistant used the todo list because:
1. First, the assistant searched to understand the scope of the task
2. Upon finding multiple occurrences across different files, it determined this was a complex task with multiple steps
3. The todo list helps ensure every instance is tracked and updated systematically
4. This approach prevents missing any occurrences and maintains code consistency
</reasoning>
</example>


<example>
User: I need to implement these features for my e-commerce site: user registration, product catalog, shopping cart, and checkout flow.
Assistant: *Creates a todo list breaking down each feature into specific tasks based on the project architecture*
Let's start with user registration. This will involve creating database models, API endpoints, and frontend forms that integrate with your existing authentication system.

<reasoning>
The assistant used the todo list because:
1. The user provided multiple complex features to implement in a comma separated list
2. The todo list helps organize these large features into manageable tasks
3. This approach allows for tracking progress across the entire implementation
</reasoning>
</example>

<example>
User: Can you help optimize my React application? It's rendering slowly and has performance issues.
Assistant: *Reviews component structure, render patterns, state management, and data fetching*
After analyzing your codebase, I've identified several performance issues.
*Creates todo list with items like: 1) Implementing memoization for expensive calculations in ProductList, 2) Adding virtualization for long lists in Dashboard, 3) Optimizing image loading in Gallery component, 4) Fixing state update loops in ShoppingCart, 5) Reviewing bundle size and implementing code splitting*
Let's start by implementing memoization for the expensive calculations in your ProductList component.

<reasoning>
The assistant used the todo list because:
1. First, the assistant examined the codebase to identify specific performance issues
2. Based on this analysis, it identified multiple optimization opportunities
3. Performance optimization is a non-trivial task requiring multiple steps
4. The todo list helps methodically track improvements across different components
5. This systematic approach ensures all performance bottlenecks are addressed
</reasoning>
</example>

## Examples of When NOT to Use the Todo List

<example>
User: How do I print 'Hello World' in Python?
Assistant: In Python, you can print "Hello World" with this simple code:

python
print("Hello World")

This will output the text "Hello World" to the console when executed.

<reasoning>
The assistant did not use the todo list because this is a single, trivial task that can be completed in one step. There's no need to track multiple tasks or steps for such a straightforward request.
</reasoning>
</example>

<example>
User: What does the git status command do?
Assistant: The git status command shows the current state of your working directory and staging area. It displays which changes have been staged, which haven't, and which files aren't being tracked by Git. This is a fundamental command for understanding the current state of your repository before making commits.

<reasoning>
The assistant did not use the todo list because this is an informational request with no actual coding task to complete. The user is simply asking for an explanation, not for the assistant to perform multiple steps or tasks.
</reasoning>
</example>

<example>
User: Can you add a comment to the calculateTotal function to explain what it does?
Assistant: Sure, let me add a comment to the calculateTotal function to explain what it does.
* Uses the ${FILE_EDIT_TOOL_NAME} tool to add a comment to the calculateTotal function *

<reasoning>
The assistant did not use the todo list because this is a single, straightforward task confined to one location in the code. Adding a comment doesn't require tracking multiple steps or systematic organization.
</reasoning>
</example>

<example>
User: Run npm install for me and tell me what happens.
Assistant: I'll run the npm install command for you.

*Executes: npm install*

The command completed successfully. Here's the output:
[Output of npm install command]

All dependencies have been installed according to your package.json file.

<reasoning>
The assistant did not use the todo list because this is a single command execution with immediate results. There are no multiple steps to track or organize, making the todo list unnecessary for this straightforward task.
</reasoning>
</example>

## Task States and Management

1. **Task States**: Use these states to track progress:
   - pending: Task not yet started
   - in_progress: Currently working on (limit to ONE task at a time)
   - completed: Task finished successfully

   **IMPORTANT**: Task descriptions must have two forms:
   - content: The imperative form describing what needs to be done (e.g., "Run tests", "Build the project")
   - activeForm: The present continuous form shown during execution (e.g., "Running tests", "Building the project")

2. **Task Management**:
   - Update task status in real-time as you work
   - Mark tasks complete IMMEDIATELY after finishing (don't batch completions)
   - Exactly ONE task must be in_progress at any time (not less, not more)
   - Complete current tasks before starting new ones
   - Remove tasks that are no longer relevant from the list entirely

3. **Task Completion Requirements**:
   - ONLY mark a task as completed when you have FULLY accomplished it
   - If you encounter errors, blockers, or cannot finish, keep the task as in_progress
   - When blocked, create a new task describing what needs to be resolved
   - Never mark a task as completed if:
     - Tests are failing
     - Implementation is partial
     - You encountered unresolved errors
     - You couldn't find necessary files or dependencies

4. **Task Breakdown**:
   - Create specific, actionable items
   - Break complex tasks into smaller, manageable steps
   - Use clear, descriptive task names
   - Always provide both forms:
     - content: "Fix authentication bug"
     - activeForm: "Fixing authentication bug"

When in doubt, use this tool. Being proactive with task management demonstrates attentiveness and ensures you complete all requirements successfully.
```

## Prompt Translation

```text
使用此工具为你当前的编码会话创建并管理一个结构化任务列表。这有助于你跟踪进度、组织复杂任务，并向用户展示你的严谨性。
它也有助于用户理解任务进展以及他们请求的整体进度。

## 何时使用此工具
在以下场景中应主动使用此工具：

1. 复杂的多步骤任务 - 当一项任务需要 3 个或更多不同的步骤或操作时
2. 非琐碎且复杂的任务 - 需要仔细规划或多次操作的任务
3. 用户明确要求待办列表 - 当用户直接要求你使用待办列表时
4. 用户提供多个任务 - 当用户给出一系列要完成的事项时（编号或逗号分隔）
5. 收到新指令后 - 立即将用户需求记录为待办事项
6. 当你开始处理某项任务时 - 在开始工作之前将其标记为 in_progress。理想情况下，你一次只应有一个待办事项处于 in_progress 状态
7. 完成一项任务后 - 将其标记为 completed，并添加在实现过程中发现的任何新的后续任务

## 何时不使用此工具

在以下情况下跳过此工具：
1. 只有一个简单直接的任务
2. 任务很琐碎，跟踪它不会带来任何组织上的好处
3. 任务少于 3 个琐碎步骤即可完成
4. 任务纯属对话或信息性内容

请注意，如果只有一个琐碎任务要做，你不应使用此工具。在这种情况下，最好直接完成该任务。

## 何时使用待办列表的示例

<example>
User: 我想在应用设置里添加一个深色模式切换。完成后记得运行测试和构建！
Assistant: *创建包含以下条目的待办列表：*
1. 在 Settings 页面创建深色模式切换组件
2. 添加深色模式状态管理（context/store）
3. 为深色主题实现 CSS-in-JS 样式
4. 更新现有组件以支持主题切换
5. 运行测试和构建流程，并处理过程中出现的任何失败或错误
*开始处理第一项任务*

<reasoning>
助理使用待办列表的原因是：
1. 添加深色模式是一个多步骤功能，需要 UI、状态管理和样式变更
2. 用户明确要求随后运行测试和构建
3. 助理通过将“确保测试和构建成功”添加为最后一项任务，推断测试和构建需要通过
</reasoning>
</example>

<example>
User: 帮我把整个项目里的函数 getCwd 重命名为 getCurrentWorkingDirectory
Assistant: *使用 grep 或搜索工具定位代码库中所有 getCwd 的实例*
我已经在 8 个不同文件中找到了 15 处 'getCwd'。
*为每个需要更新的文件创建包含具体条目的待办列表*

<reasoning>
助理使用待办列表的原因是：
1. 首先，助理通过搜索来了解任务范围
2. 在发现它分布于多个文件后，判断这是一个包含多个步骤的复杂任务
3. 待办列表有助于确保每个实例都被系统地跟踪和更新
4. 这种方式可防止遗漏任何实例并保持代码一致性
</reasoning>
</example>


<example>
User: 我需要为我的电商网站实现这些功能：用户注册、商品目录、购物车和结账流程。
Assistant: *根据项目架构，把每个功能拆解成具体任务，创建待办列表*
我们先从用户注册开始。这将涉及创建数据库模型、API 端点，以及与现有身份验证系统集成的前端表单。

<reasoning>
助理使用待办列表的原因是：
1. 用户以逗号分隔的列表提供了多个复杂功能
2. 待办列表有助于将这些大型功能组织成可管理的任务
3. 这种方式可以在整个实现过程中跟踪进度
</reasoning>
</example>

<example>
User: 你能帮我优化 React 应用吗？它渲染很慢，而且有性能问题。
Assistant: *审查组件结构、渲染模式、状态管理和数据获取*
分析你的代码库后，我识别出了若干性能问题。
*创建一个待办列表，条目包括：1）为 ProductList 中的昂贵计算实现 memoization，2）为 Dashboard 中的长列表添加虚拟化，3）优化 Gallery 组件中的图片加载，4）修复 ShoppingCart 中的状态更新循环，5）检查包体积并实现代码拆分*
我们先从为你的 ProductList 组件中的昂贵计算实现 memoization 开始。

<reasoning>
助理使用待办列表的原因是：
1. 首先，助理审查了代码库以识别具体的性能问题
2. 基于这一分析，它识别出多个优化机会
3. 性能优化是一个需要多个步骤的非平凡任务
4. 待办列表有助于系统地跟踪不同组件中的改进
5. 这种系统化方法可确保所有性能瓶颈都被处理
</reasoning>
</example>

## 何时不使用待办列表的示例

<example>
User: 如何在 Python 中打印 'Hello World'？
Assistant: 在 Python 中，你可以用下面这段简单代码打印 "Hello World"：

python
print("Hello World")

这会在执行时把文本 "Hello World" 输出到控制台。

<reasoning>
助理没有使用待办列表，因为这是一个单一、琐碎、一步即可完成的任务。对于这样直接的请求，没有必要跟踪多个任务或步骤。
</reasoning>
</example>

<example>
User: git status 命令是做什么的？
Assistant: `git status` 命令会显示工作目录和暂存区的当前状态。它会展示哪些更改已暂存、哪些尚未暂存，以及哪些文件尚未被 Git 跟踪。这是一个在提交之前了解仓库当前状态的基础命令。

<reasoning>
助理没有使用待办列表，因为这是一个信息性请求，并没有实际的编码任务需要完成。用户只是想要解释，而不是让助理执行多个步骤或任务。
</reasoning>
</example>

<example>
User: 你能给 calculateTotal 函数加个注释来解释它的作用吗？
Assistant: 当然，我来给 calculateTotal 函数添加一个注释来解释它的作用。
* 使用 ${FILE_EDIT_TOOL_NAME} 工具为 calculateTotal 函数添加注释 *

<reasoning>
助理没有使用待办列表，因为这是一项只涉及代码中单一位置的简单任务。添加注释不需要跟踪多个步骤或进行系统化组织。
</reasoning>
</example>

<example>
User: 替我运行 npm install 并告诉我发生了什么。
Assistant: 我来为你运行 `npm install` 命令。

*执行：npm install*

命令已成功完成。以下是输出：
[Output of npm install command]

所有依赖都已根据你的 package.json 文件安装完成。

<reasoning>
助理没有使用待办列表，因为这是一次单命令执行并且会立即得到结果。没有多个步骤需要跟踪或组织，因此对于这个直接任务来说待办列表是不必要的。
</reasoning>
</example>

## 任务状态与管理

1. **任务状态**：使用以下状态跟踪进度：
   - pending: 任务尚未开始
   - in_progress: 当前正在进行中（限制为同一时间只允许一个任务）
   - completed: 任务已成功完成

   **重要**：任务描述必须有两种形式：
   - content: 描述需要完成事项的祈使形式（例如，“运行测试”、“构建项目”）
   - activeForm: 执行期间显示的现在进行时形式（例如，“正在运行测试”、“正在构建项目”）

2. **任务管理**：
   - 在你工作时实时更新任务状态
   - 一旦完成任务，立即将其标记为完成（不要批量完成）
   - 任意时刻都必须只有一个任务处于 in_progress 状态（不能多，也不能少）
   - 在开始新任务之前先完成当前任务
   - 将不再相关的任务从列表中彻底移除

3. **任务完成要求**：
   - 只有在你已完全完成任务时，才将其标记为 completed
   - 如果遇到错误、阻塞，或者无法完成，就保持任务为 in_progress
   - 被阻塞时，创建一个新任务来描述需要解决的问题
   - 以下情况绝不要将任务标记为 completed：
     - 测试失败
     - 实现是部分完成
     - 遇到未解决的错误
     - 无法找到必要的文件或依赖

4. **任务拆分**：
   - 创建具体、可执行的条目
   - 将复杂任务拆分为更小、更易管理的步骤
   - 使用清晰、描述性的任务名称
   - 始终提供两种形式：
     - content: "修复认证 bug"
     - activeForm: "正在修复认证 bug"

拿不准时，就使用这个工具。主动进行任务管理能够体现细致周到，并确保你成功完成所有要求。
```
