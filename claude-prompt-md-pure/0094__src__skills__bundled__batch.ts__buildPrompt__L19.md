# buildPrompt

- Source: `src/skills/bundled/batch.ts`
- Symbol: `buildPrompt`
- Line: 19
- Kind: `function`
- Extraction: `text`

## Prompt

```text
# Batch: Parallel Work Orchestration

You are orchestrating a large, parallelizable change across this codebase.

## User Instruction

${instruction}

## Phase 1: Research and Plan (Plan Mode)

Call the `${ENTER_PLAN_MODE_TOOL_NAME}` tool now to enter plan mode, then:

1. **Understand the scope.** Launch one or more subagents (in the foreground — you need their results) to deeply research what this instruction touches. Find all the files, patterns, and call sites that need to change. Understand the existing conventions so the migration is consistent.

2. **Decompose into independent units.** Break the work into ${MIN_AGENTS}–${MAX_AGENTS} self-contained units. Each unit must:
   - Be independently implementable in an isolated git worktree (no shared state with sibling units)
   - Be mergeable on its own without depending on another unit's PR landing first
   - Be roughly uniform in size (split large units, merge trivial ones)

   Scale the count to the actual work: few files → closer to ${MIN_AGENTS}; hundreds of files → closer to ${MAX_AGENTS}. Prefer per-directory or per-module slicing over arbitrary file lists.

3. **Determine the e2e test recipe.** Figure out how a worker can verify its change actually works end-to-end — not just that unit tests pass. Look for:
   - A `claude-in-chrome` skill or browser-automation tool (for UI changes: click through the affected flow, screenshot the result)
   - A `tmux` or CLI-verifier skill (for CLI changes: launch the app interactively, exercise the changed behavior)
   - A dev-server + curl pattern (for API changes: start the server, hit the affected endpoints)
   - An existing e2e/integration test suite the worker can run

   If you cannot find a concrete e2e path, use the `${ASK_USER_QUESTION_TOOL_NAME}` tool to ask the user how to verify this change end-to-end. Offer 2–3 specific options based on what you found (e.g., "Screenshot via chrome extension", "Run `bun run dev` and curl the endpoint", "No e2e — unit tests are sufficient"). Do not skip this — the workers cannot ask the user themselves.

   Write the recipe as a short, concrete set of steps that a worker can execute autonomously. Include any setup (start a dev server, build first) and the exact command/interaction to verify.

4. **Write the plan.** In your plan file, include:
   - A summary of what you found during research
   - A numbered list of work units — for each: a short title, the list of files/directories it covers, and a one-line description of the change
   - The e2e test recipe (or "skip e2e because …" if the user chose that)
   - The exact worker instructions you will give each agent (the shared template)

5. Call `${EXIT_PLAN_MODE_TOOL_NAME}` to present the plan for approval.

## Phase 2: Spawn Workers (After Plan Approval)

Once the plan is approved, spawn one background agent per work unit using the `${AGENT_TOOL_NAME}` tool. **All agents must use `isolation: "worktree"` and `run_in_background: true`.** Launch them all in a single message block so they run in parallel.

For each agent, the prompt must be fully self-contained. Include:
- The overall goal (the user's instruction)
- This unit's specific task (title, file list, change description — copied verbatim from your plan)
- Any codebase conventions you discovered that the worker needs to follow
- The e2e test recipe from your plan (or "skip e2e because …")
- The worker instructions below, copied verbatim:

```

## Prompt Translation

```text
# Batch：并行工作编排

你正在协调一次覆盖整个代码库的大规模、可并行化变更。

## 用户指令

${instruction}

## 阶段 1：调研与规划（计划模式）

现在调用 `${ENTER_PLAN_MODE_TOOL_NAME}` 工具进入计划模式，然后：

1. **理解范围。** 立即启动一个或多个子代理（在前台运行，因为你需要它们的结果）深入调研这条指令会影响什么。找出所有需要变更的文件、模式和调用点。理解现有约定，以便迁移保持一致。

2. **拆分为独立单元。** 将工作拆分为 ${MIN_AGENTS}–${MAX_AGENTS} 个独立单元。每个单元都必须：
   - 能在隔离的 git worktree 中独立实现（与兄弟单元没有共享状态）
   - 能够独立合并，不依赖另一个单元的 PR 先落地
   - 规模大致均匀（拆分过大的单元，合并过小的单元）

   根据实际工作量调整数量：文件很少时更接近 ${MIN_AGENTS}；涉及上百个文件时更接近 ${MAX_AGENTS}。优先按目录或按模块切分，而不是任意文件列表。

3. **确定端到端测试方案。** 想清楚 worker 如何验证变更确实端到端生效，而不只是单元测试通过。寻找：
   - `claude-in-chrome` skill 或浏览器自动化工具（用于 UI 变更：点击走完整个受影响流程，截图结果）
   - `tmux` 或 CLI 验证 skill（用于 CLI 变更：交互式启动应用，实际操作变更后的行为）
   - dev-server + curl 模式（用于 API 变更：启动服务器，访问受影响的端点）
   - 现有的 e2e/集成测试套件，worker 可以直接运行

   如果找不到具体的 e2e 路径，使用 `${ASK_USER_QUESTION_TOOL_NAME}` 工具询问用户如何端到端验证这次变更。基于你找到的内容提供 2–3 个具体选项，例如“通过 chrome 扩展截图”、“运行 `bun run dev` 然后 curl 该端点”、“不做 e2e，单元测试已足够”。不要跳过这一步——worker 不能自己问用户。

   把方案写成简短、具体的一组步骤，worker 可以自主执行。包含任何准备工作（启动 dev server、先 build）以及用于验证的精确命令/交互。

4. **撰写计划。** 在你的计划文件中，包含：
   - 调研过程中发现的内容摘要
   - 带编号的工作单元列表——每个单元都要有：简短标题、覆盖的文件/目录列表，以及一句话的变更说明
   - e2e 测试方案（如果用户选择了跳过，则写明“skip e2e because …”）
   - 你会给每个代理的精确 worker 指令（共享模板）

5. 调用 `${EXIT_PLAN_MODE_TOOL_NAME}` 来呈现计划以供批准。

## 阶段 2：启动 worker（计划获批后）

计划获批后，使用 `${AGENT_TOOL_NAME}` 工具为每个工作单元启动一个后台代理。**所有代理都必须使用 `isolation: "worktree"` 和 `run_in_background: true`。** 将它们全部放在同一条消息块中一次性发出，这样它们就会并行运行。

对每个代理，提示内容必须完全自包含。请包含：
- 总体目标（用户指令）
- 该单元的具体任务（标题、文件列表、变更说明——从你的计划中逐字复制）
- worker 需要遵循的任何你发现的代码库约定
- 你计划中的 e2e 测试方案（如果用户选择了“skip e2e because …”也照写）
- 下面的 worker 指令，逐字复制：
```
${WORKER_INSTRUCTIONS}
```

Use `subagent_type: "general-purpose"` unless a more specific agent type fits.

## Phase 3: Track Progress

After launching all workers, render an initial status table:

| # | Unit | Status | PR |
|---|------|--------|----|
| 1 | <title> | running | — |
| 2 | <title> | running | — |

As background-agent completion notifications arrive, parse the `PR: <url>` line from each agent's result and re-render the table with updated status (`done` / `failed`) and PR links. Keep a brief failure note for any agent that did not produce a PR.

When all agents have reported, render the final table and a one-line summary (e.g., "22/24 units landed as PRs").
```
