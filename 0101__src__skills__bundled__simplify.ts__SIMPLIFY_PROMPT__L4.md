# SIMPLIFY_PROMPT

- Source: `src/skills/bundled/simplify.ts`
- Symbol: `SIMPLIFY_PROMPT`
- Line: 4
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
# Simplify: Code Review and Cleanup

Review all changed files for reuse, quality, and efficiency. Fix any issues found.

## Phase 1: Identify Changes

Run `git diff` (or `git diff HEAD` if there are staged changes) to see what changed. If there are no git changes, review the most recently modified files that the user mentioned or that you edited earlier in this conversation.

## Phase 2: Launch Three Review Agents in Parallel

Use the ${AGENT_TOOL_NAME} tool to launch all three agents concurrently in a single message. Pass each agent the full diff so it has the complete context.

### Agent 1: Code Reuse Review

For each change:

1. **Search for existing utilities and helpers** that could replace newly written code. Look for similar patterns elsewhere in the codebase — common locations are utility directories, shared modules, and files adjacent to the changed ones.
2. **Flag any new function that duplicates existing functionality.** Suggest the existing function to use instead.
3. **Flag any inline logic that could use an existing utility** — hand-rolled string manipulation, manual path handling, custom environment checks, ad-hoc type guards, and similar patterns are common candidates.

### Agent 2: Code Quality Review

Review the same changes for hacky patterns:

1. **Redundant state**: state that duplicates existing state, cached values that could be derived, observers/effects that could be direct calls
2. **Parameter sprawl**: adding new parameters to a function instead of generalizing or restructuring existing ones
3. **Copy-paste with slight variation**: near-duplicate code blocks that should be unified with a shared abstraction
4. **Leaky abstractions**: exposing internal details that should be encapsulated, or breaking existing abstraction boundaries
5. **Stringly-typed code**: using raw strings where constants, enums (string unions), or branded types already exist in the codebase
6. **Unnecessary JSX nesting**: wrapper Boxes/elements that add no layout value — check if inner component props (flexShrink, alignItems, etc.) already provide the needed behavior
7. **Unnecessary comments**: comments explaining WHAT the code does (well-named identifiers already do that), narrating the change, or referencing the task/caller — delete; keep only non-obvious WHY (hidden constraints, subtle invariants, workarounds)

### Agent 3: Efficiency Review

Review the same changes for efficiency:

1. **Unnecessary work**: redundant computations, repeated file reads, duplicate network/API calls, N+1 patterns
2. **Missed concurrency**: independent operations run sequentially when they could run in parallel
3. **Hot-path bloat**: new blocking work added to startup or per-request/per-render hot paths
4. **Recurring no-op updates**: state/store updates inside polling loops, intervals, or event handlers that fire unconditionally — add a change-detection guard so downstream consumers aren't notified when nothing changed. Also: if a wrapper function takes an updater/reducer callback, verify it honors same-reference returns (or whatever the "no change" signal is) — otherwise callers' early-return no-ops are silently defeated
5. **Unnecessary existence checks**: pre-checking file/resource existence before operating (TOCTOU anti-pattern) — operate directly and handle the error
6. **Memory**: unbounded data structures, missing cleanup, event listener leaks
7. **Overly broad operations**: reading entire files when only a portion is needed, loading all items when filtering for one

## Phase 3: Fix Issues

Wait for all three agents to complete. Aggregate their findings and fix each issue directly. If a finding is a false positive or not worth addressing, note it and move on — do not argue with the finding, just skip it.

When done, briefly summarize what was fixed (or confirm the code was already clean).
```

## Prompt Translation

```text
# Simplify：代码审查与清理

审查所有变更文件，检查可复用性、质量和效率。修复发现的任何问题。

## 第 1 阶段：识别变更

运行 `git diff`（如果有暂存变更，则运行 `git diff HEAD`）来查看发生了什么变化。如果没有 git 变更，则审查用户提到的、或你在本次对话中较早编辑过的最近修改文件。

## 第 2 阶段：并行启动三个审查代理

使用 `${AGENT_TOOL_NAME}` 工具在一条消息中同时启动这三个代理。把完整 diff 传给每个代理，让它们拥有完整上下文。

### 代理 1：代码复用审查

对每一处变更：

1. **搜索现有的工具函数和辅助函数**，看看是否可以替换新写的代码。留意代码库中的相似模式，常见位置包括工具目录、共享模块，以及变更文件附近的文件。
2. **标记任何重复已有功能的新函数。** 建议改用现有函数。
3. **标记任何可以使用现有工具函数的内联逻辑** - 手写的字符串处理、手动路径处理、自定义环境检查、临时的类型守卫，以及类似模式，都是常见候选。

### 代理 2：代码质量审查

针对相同的变更，检查以下不够优雅的模式：

1. **冗余状态**：重复已有状态的状态、可以派生出来却被缓存的值、可以直接调用却被做成观察器/副作用的逻辑
2. **参数膨胀**：通过给函数增加新参数来解决问题，而不是泛化或重构现有设计
3. **仅有细微差异的复制粘贴**：几乎重复的代码块，应该通过共享抽象统一起来
4. **抽象泄漏**：暴露了本应封装的内部细节，或破坏了既有的抽象边界
5. **字符串化代码**：在代码库中已有常量、枚举（字符串联合）或品牌类型时，却使用原始字符串
6. **不必要的 JSX 嵌套**：添加了没有布局价值的包装 `Box`/元素 - 检查内层组件属性（`flexShrink`、`alignItems` 等）是否已经能提供所需行为
7. **不必要的注释**：解释代码“做了什么”的注释（良好命名的标识符已经足够），叙述变更过程，或引用任务/调用方的注释 - 删除；只保留不明显的“为什么”（隐藏约束、微妙不变量、绕过方案）

### 代理 3：效率审查

针对相同的变更，检查效率问题：

1. **不必要的工作**：冗余计算、重复文件读取、重复的网络/API 调用、N+1 模式
2. **错失并发**：独立操作按顺序执行，而其实可以并行
3. **热路径臃肿**：在启动路径或每次请求/每次渲染的热路径中加入了新的阻塞工作
4. **重复的无操作更新**：轮询循环、定时器或事件处理器中无条件触发的 state/store 更新 - 添加变更检测守卫，这样下游消费者在没有变化时就不会被通知。另外：如果某个包装函数接受 updater/reducer 回调，确认它是否尊重相同引用返回（或者其他表示“无变化”的信号） - 否则调用方的提前返回式 no-op 会被悄悄抵消
5. **不必要的存在性检查**：在操作前先检查文件/资源是否存在（TOCTOU 反模式） - 直接操作并处理错误
6. **内存问题**：无界数据结构、缺少清理、事件监听器泄漏
7. **过宽操作**：只需要一部分时却读取整个文件，或在只过滤单个项时加载所有项

## 第 3 阶段：修复问题

等待三个代理全部完成。汇总它们的发现并直接修复每个问题。如果某个发现是误报，或者不值得处理，就记下并继续 - 不要与发现争论，直接跳过。

完成后，简要总结修复了什么（或者确认代码本来就已经很干净）。
```
