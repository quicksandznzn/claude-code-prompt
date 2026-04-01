# NEW_INIT_PROMPT

- Source: `src/commands/init.ts`
- Symbol: `NEW_INIT_PROMPT`
- Line: 28
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Set up a minimal CLAUDE.md (and optionally skills and hooks) for this repo. CLAUDE.md is loaded into every Claude Code session, so it must be concise — only include what Claude would get wrong without it.

## Phase 1: Ask what to set up

Use AskUserQuestion to find out what the user wants:

- "Which CLAUDE.md files should /init set up?"
  Options: "Project CLAUDE.md" | "Personal CLAUDE.local.md" | "Both project + personal"
  Description for project: "Team-shared instructions checked into source control — architecture, coding standards, common workflows."
  Description for personal: "Your private preferences for this project (gitignored, not shared) — your role, sandbox URLs, preferred test data, workflow quirks."

- "Also set up skills and hooks?"
  Options: "Skills + hooks" | "Skills only" | "Hooks only" | "Neither, just CLAUDE.md"
  Description for skills: "On-demand capabilities you or Claude invoke with `/skill-name` — good for repeatable workflows and reference knowledge."
  Description for hooks: "Deterministic shell commands that run on tool events (e.g., format after every edit). Claude can't skip them."

## Phase 2: Explore the codebase

Launch a subagent to survey the codebase, and ask it to read key files to understand the project: manifest files (package.json, Cargo.toml, pyproject.toml, go.mod, pom.xml, etc.), README, Makefile/build configs, CI config, existing CLAUDE.md, .claude/rules/, AGENTS.md, .cursor/rules or .cursorrules, .github/copilot-instructions.md, .windsurfrules, .clinerules, .mcp.json.

Detect:
- Build, test, and lint commands (especially non-standard ones)
- Languages, frameworks, and package manager
- Project structure (monorepo with workspaces, multi-module, or single project)
- Code style rules that differ from language defaults
- Non-obvious gotchas, required env vars, or workflow quirks
- Existing .claude/skills/ and .claude/rules/ directories
- Formatter configuration (prettier, biome, ruff, black, gofmt, rustfmt, or a unified format script like `npm run format` / `make fmt`)
- Git worktree usage: run `git worktree list` to check if this repo has multiple worktrees (only relevant if the user wants a personal CLAUDE.local.md)

Note what you could NOT figure out from code alone — these become interview questions.

## Phase 3: Fill in the gaps

Use AskUserQuestion to gather what you still need to write good CLAUDE.md files and skills. Ask only things the code can't answer.

If the user chose project CLAUDE.md or both: ask about codebase practices — non-obvious commands, gotchas, branch/PR conventions, required env setup, testing quirks. Skip things already in README or obvious from manifest files. Do not mark any options as "recommended" — this is about how their team works, not best practices.

If the user chose personal CLAUDE.local.md or both: ask about them, not the codebase. Do not mark any options as "recommended" — this is about their personal preferences, not best practices. Examples of questions:
  - What's their role on the team? (e.g., "backend engineer", "data scientist", "new hire onboarding")
  - How familiar are they with this codebase and its languages/frameworks? (so Claude can calibrate explanation depth)
  - Do they have personal sandbox URLs, test accounts, API key paths, or local setup details Claude should know?
  - Only if Phase 2 found multiple git worktrees: ask whether their worktrees are nested inside the main repo (e.g., `.claude/worktrees/<name>/`) or siblings/external (e.g., `../myrepo-feature/`). If nested, the upward file walk finds the main repo's CLAUDE.local.md automatically — no special handling needed. If sibling/external, the personal content should live in a home-directory file (e.g., `~/.claude/<project-name>-instructions.md`) and each worktree gets a one-line CLAUDE.local.md stub that imports it: `@~/.claude/<project-name>-instructions.md`. Never put this import in the project CLAUDE.md — that would check a personal reference into the team-shared file.
  - Any communication preferences? (e.g., "be terse", "always explain tradeoffs", "don't summarize at the end")

**Synthesize a proposal from Phase 2 findings** — e.g., format-on-edit if a formatter exists, a `/verify` skill if tests exist, a CLAUDE.md note for anything from the gap-fill answers that's a guideline rather than a workflow. For each, pick the artifact type that fits, **constrained by the Phase 1 skills+hooks choice**:

  - **Hook** (stricter) — deterministic shell command on a tool event; Claude can't skip it. Fits mechanical, fast, per-edit steps: formatting, linting, running a quick test on the changed file.
  - **Skill** (on-demand) — you or Claude invoke `/skill-name` when you want it. Fits workflows that don't belong on every edit: deep verification, session reports, deploys.
  - **CLAUDE.md note** (looser) — influences Claude's behavior but not enforced. Fits communication/thinking preferences: "plan before coding", "be terse", "explain tradeoffs".

  **Respect Phase 1's skills+hooks choice as a hard filter**: if the user picked "Skills only", downgrade any hook you'd suggest to a skill or a CLAUDE.md note. If "Hooks only", downgrade skills to hooks (where mechanically possible) or notes. If "Neither", everything becomes a CLAUDE.md note. Never propose an artifact type the user didn't opt into.

**Show the proposal via AskUserQuestion's `preview` field, not as a separate text message** — the dialog overlays your output, so preceding text is hidden. The `preview` field renders markdown in a side-panel (like plan mode); the `question` field is plain-text-only. Structure it as:

  - `question`: short and plain, e.g. "Does this proposal look right?"
  - Each option gets a `preview` with the full proposal as markdown. The "Looks good — proceed" option's preview shows everything; per-item-drop options' previews show what remains after that drop.
  - **Keep previews compact — the preview box truncates with no scrolling.** One line per item, no blank lines between items, no header. Example preview content:

    • **Format-on-edit hook** (automatic) — `ruff format <file>` via PostToolUse
    • **/verify skill** (on-demand) — `make lint && make typecheck && make test`
    • **CLAUDE.md note** (guideline) — "run lint/typecheck/test before marking done"

  - Option labels stay short ("Looks good", "Drop the hook", "Drop the skill") — the tool auto-adds an "Other" free-text option, so don't add your own catch-all.

**Build the preference queue** from the accepted proposal. Each entry: {type: hook|skill|note, description, target file, any Phase-2-sourced details like the actual test/format command}. Phases 4-7 consume this queue.

## Phase 4: Write CLAUDE.md (if user chose project or both)

Write a minimal CLAUDE.md at the project root. Every line must pass this test: "Would removing this cause Claude to make mistakes?" If no, cut it.

**Consume `note` entries from the Phase 3 preference queue whose target is CLAUDE.md** (team-level notes) — add each as a concise line in the most relevant section. These are the behaviors the user wants Claude to follow but didn't need guaranteed (e.g., "propose a plan before implementing", "explain the tradeoffs when refactoring"). Leave personal-targeted notes for Phase 5.

Include:
- Build/test/lint commands Claude can't guess (non-standard scripts, flags, or sequences)
- Code style rules that DIFFER from language defaults (e.g., "prefer type over interface")
- Testing instructions and quirks (e.g., "run single test with: pytest -k 'test_name'")
- Repo etiquette (branch naming, PR conventions, commit style)
- Required env vars or setup steps
- Non-obvious gotchas or architectural decisions
- Important parts from existing AI coding tool configs if they exist (AGENTS.md, .cursor/rules, .cursorrules, .github/copilot-instructions.md, .windsurfrules, .clinerules)

Exclude:
- File-by-file structure or component lists (Claude can discover these by reading the codebase)
- Standard language conventions Claude already knows
- Generic advice ("write clean code", "handle errors")
- Detailed API docs or long references — use `@path/to/import` syntax instead (e.g., `@docs/api-reference.md`) to inline content on demand without bloating CLAUDE.md
- Information that changes frequently — reference the source with `@path/to/import` so Claude always reads the current version
- Long tutorials or walkthroughs (move to a separate file and reference with `@path/to/import`, or put in a skill)
- Commands obvious from manifest files (e.g., standard "npm test", "cargo test", "pytest")

Be specific: "Use 2-space indentation in TypeScript" is better than "Format code properly."

Do not repeat yourself and do not make up sections like "Common Development Tasks" or "Tips for Development" — only include information expressly found in files you read.

Prefix the file with:

```

## Prompt Translation

```text
为这个仓库设置一个最小化的 CLAUDE.md（以及可选的 skills 和 hooks）。CLAUDE.md 会被加载到每个 Claude Code 会话中，所以它必须简洁 - 只包含那些如果没有它 Claude 就会搞错的内容。

## 阶段 1：询问要设置什么

使用 AskUserQuestion 了解用户想要什么：

- "Which CLAUDE.md files should /init set up?"
  Options: "Project CLAUDE.md" | "Personal CLAUDE.local.md" | "Both project + personal"
  Description for project: "写入源代码管理、由团队共享的指令 - 架构、编码规范、常见工作流。"
  Description for personal: "你针对这个项目的私有偏好（被 gitignore，不共享） - 你的角色、sandbox URLs、偏好的测试数据、工作流上的特殊习惯。"

- "Also set up skills and hooks?"
  Options: "Skills + hooks" | "Skills only" | "Hooks only" | "Neither, just CLAUDE.md"
  Description for skills: "可按需调用的能力，你或 Claude 可以用 `/skill-name` 触发 - 适合可重复的工作流和参考性知识。"
  Description for hooks: "在工具事件上运行的确定性 shell 命令（例如，每次编辑后格式化）。Claude 不能跳过它们。"

## 阶段 2：探索代码库

启动一个子代理来巡查代码库，并让它读取关键文件以理解项目：清单文件（package.json、Cargo.toml、pyproject.toml、go.mod、pom.xml 等）、README、Makefile/build 配置、CI 配置、现有 CLAUDE.md、.claude/rules/、AGENTS.md、.cursor/rules 或 .cursorrules、.github/copilot-instructions.md、.windsurfrules、.clinerules、.mcp.json。

检测：
- 构建、测试和 lint 命令（尤其是非标准命令）
- 语言、框架和包管理器
- 项目结构（monorepo with workspaces、多模块，或单体项目）
- 与语言默认值不同的代码风格规则
- 非显而易见的坑、必需的环境变量，或工作流上的特殊习惯
- 现有的 .claude/skills/ 和 .claude/rules/ 目录
- 格式化器配置（prettier、biome、ruff、black、gofmt、rustfmt，或统一的格式化脚本，比如 `npm run format` / `make fmt`）
- Git worktree 的使用：运行 `git worktree list` 检查这个仓库是否有多个 worktree（仅当用户想要个人 CLAUDE.local.md 时才相关）

记录那些你无法仅从代码中弄清楚的内容 - 这些会变成访谈问题。

## 阶段 3：补齐空白

使用 AskUserQuestion 收集你仍然需要的信息，以便写出好的 CLAUDE.md 文件和 skills。只问代码无法回答的问题。

如果用户选择了 project CLAUDE.md 或 both：询问代码库实践 - 非显而易见的命令、坑、分支/PR 规范、必需的环境设置、测试上的特殊习惯。跳过 README 中已经写明的内容或从清单文件里显而易见的内容。不要把任何选项标记为 "recommended" - 这里问的是他们团队的工作方式，不是最佳实践。

如果用户选择了 personal CLAUDE.local.md 或 both：询问他们本人，而不是代码库。不要把任何选项标记为 "recommended" - 这里问的是他们个人偏好，不是最佳实践。示例问题：
  - 他们在团队里的角色是什么？（例如，"后端工程师"、"数据科学家"、"新员工入职"）
  - 他们对这个代码库及其语言/框架有多熟悉？（这样 Claude 可以调整解释深度）
  - 他们是否有 Claude 应该知道的个人 sandbox URLs、测试账号、API key 路径或本地设置细节？
  - 只有当阶段 2 发现了多个 git worktree 时：询问他们的 worktree 是嵌套在主仓库内部（例如，`.claude/worktrees/<name>/`）还是兄弟目录/外部（例如，`../myrepo-feature/`）。如果是嵌套的，向上查找文件会自动找到主仓库的 CLAUDE.local.md - 不需要特殊处理。如果是兄弟目录/外部，个人内容应放在一个 home 目录文件里（例如，`~/.claude/<project-name>-instructions.md`），并且每个 worktree 都有一个一行的 CLAUDE.local.md stub 来导入它：`@~/.claude/<project-name>-instructions.md`。绝不要把这个导入写进项目 CLAUDE.md - 那会把个人引用检查入团队共享文件。
  - 还有没有沟通偏好？（例如，"简洁一点"、"总是解释权衡"、"最后不要总结"）

**根据阶段 2 的发现综合出一个提案** - 例如，如果存在格式化器，就提议在编辑后自动格式化；如果存在测试，就提议一个 `/verify` skill；如果 gap-fill 答案里有任何更像指导原则而不是工作流的内容，就提议写进 CLAUDE.md。对于每一项，选择最合适的 artifact 类型，并且**受阶段 1 的 skills+hooks 选择约束**：

  - **Hook**（更严格） - 在工具事件上运行的确定性 shell 命令；Claude 不能跳过。适合机械、快速、每次编辑都要做的步骤：格式化、lint、针对改动文件运行一个快速测试。
  - **Skill**（按需） - 你或 Claude 在需要时用 `/skill-name` 触发。适合不该每次编辑都运行的工作流：深度验证、会话报告、部署。
  - **CLAUDE.md note**（更宽松） - 会影响 Claude 的行为，但不受强制执行。适合沟通/思考偏好："先计划再编码"、"简洁一点"、"解释权衡"。

  **把阶段 1 的 skills+hooks 选择当作硬性过滤器来遵守**：如果用户选了 "Skills only"，把你原本会建议的任何 hook 降级为 skill 或 CLAUDE.md note。如果是 "Hooks only"，把 skills 降级为 hooks（在机械上可行时）或 notes。如果是 "Neither"，所有内容都变成 CLAUDE.md note。绝不要提出用户没有选中的 artifact 类型。

**通过 AskUserQuestion 的 `preview` 字段展示提案，而不是单独发文本消息** - 这个对话会覆盖你的输出，所以前面的文本会被隐藏。`preview` 字段会在侧边栏渲染 markdown（类似 plan mode）；`question` 字段只能是纯文本。结构如下：

  - `question`：简短、直接，例如 "Does this proposal look right?"
  - 每个选项都带一个 `preview`，其中包含完整提案的 markdown。"Looks good — proceed" 选项的 preview 要展示全部内容；每个删除某项的选项 preview 要展示删除之后剩下的内容。
  - **保持 previews 简洁 - 预览框会截断，而且不能滚动。** 每项一行，项目之间不要空行，不要标题。示例 preview 内容：

    • **Format-on-edit hook**（自动） - 通过 PostToolUse 运行 `ruff format <file>`
    • **/verify skill**（按需） - `make lint && make typecheck && make test`
    • **CLAUDE.md note**（指导原则） - "在标记完成前运行 lint/typecheck/test"

  - 选项标签保持简短（"Looks good"、"Drop the hook"、"Drop the skill"） - 工具会自动添加一个 "Other" 自由输入选项，所以不要自己再加一个兜底选项。

**根据接受的提案构建 preference queue。** 每个条目：{type: hook|skill|note, description, target file, 以及任何来自阶段 2 的细节，比如真实的测试/格式化命令}。第 4-7 阶段会消费这个队列。

## 阶段 4：写 CLAUDE.md（如果用户选择了 project 或 both）

在项目根目录写一个最小化的 CLAUDE.md。每一行都必须通过这个测试："如果删掉它，Claude 会不会更容易犯错？" 如果不会，就删掉。

**消费阶段 3 的 preference queue 中目标是 CLAUDE.md 的 `note` 条目**（团队级笔记） - 把每一条作为简洁的一行添加到最相关的部分。这些是用户希望 Claude 遵循、但不需要强制保证的行为（例如，"实现前先提出计划"、"重构时解释权衡"）。把面向个人的 notes 留到阶段 5。

包含：
- Claude 无法猜到的构建/测试/lint 命令（非标准脚本、标志或顺序）
- 与语言默认值不同的代码风格规则（例如，"prefer type over interface"）
- 测试说明和特殊习惯（例如，"run single test with: pytest -k 'test_name'"）
- 仓库礼仪（分支命名、PR 规范、提交风格）
- 必需的环境变量或设置步骤
- 非显而易见的坑或架构决策
- 如果存在任何重要的 AI 编码工具配置，也要包含其中的重要部分（AGENTS.md、.cursor/rules、.cursorrules、.github/copilot-instructions.md、.windsurfrules、.clinerules）

排除：
- 按文件划分的结构或组件列表（Claude 可以通过阅读代码库自己发现）
- Claude 已经知道的标准语言约定
- 通用建议（"写干净代码"、"处理错误"）
- 详细 API 文档或长篇参考资料 - 用 `@path/to/import` 语法替代（例如，`@docs/api-reference.md`），这样可以按需内联内容而不会让 CLAUDE.md 变得臃肿
- 频繁变化的信息 - 用 `@path/to/import` 引用源文件，这样 Claude 总会读取当前版本
- 冗长的教程或操作指南（移动到单独文件并用 `@path/to/import` 引用，或者放进 skill）
- 从清单文件里显而易见的命令（例如，标准的 "npm test"、"cargo test"、"pytest"）

要具体："TypeScript 里使用 2 空格缩进" 比 "正确格式化代码" 更好。

不要重复，也不要编造像 "Common Development Tasks" 或 "Tips for Development" 这样的章节 - 只包含你读过的文件里明确存在的信息。

以下内容作为文件前缀：
```
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.
```

If CLAUDE.md already exists: read it, propose specific changes as diffs, and explain why each change improves it. Do not silently overwrite.

For projects with multiple concerns, suggest organizing instructions into `.claude/rules/` as separate focused files (e.g., `code-style.md`, `testing.md`, `security.md`). These are loaded automatically alongside CLAUDE.md and can be scoped to specific file paths using `paths` frontmatter.

For projects with distinct subdirectories (monorepos, multi-module projects, etc.): mention that subdirectory CLAUDE.md files can be added for module-specific instructions (they're loaded automatically when Claude works in those directories). Offer to create them if the user wants.

## Phase 5: Write CLAUDE.local.md (if user chose personal or both)

Write a minimal CLAUDE.local.md at the project root. This file is automatically loaded alongside CLAUDE.md. After creating it, add `CLAUDE.local.md` to the project's .gitignore so it stays private.

**Consume `note` entries from the Phase 3 preference queue whose target is CLAUDE.local.md** (personal-level notes) — add each as a concise line. If the user chose personal-only in Phase 1, this is the sole consumer of note entries.

Include:
- The user's role and familiarity with the codebase (so Claude can calibrate explanations)
- Personal sandbox URLs, test accounts, or local setup details
- Personal workflow or communication preferences

Keep it short — only include what would make Claude's responses noticeably better for this user.

If Phase 2 found multiple git worktrees and the user confirmed they use sibling/external worktrees (not nested inside the main repo): the upward file walk won't find a single CLAUDE.local.md from all worktrees. Write the actual personal content to `~/.claude/<project-name>-instructions.md` and make CLAUDE.local.md a one-line stub that imports it: `@~/.claude/<project-name>-instructions.md`. The user can copy this one-line stub to each sibling worktree. Never put this import in the project CLAUDE.md. If worktrees are nested inside the main repo (e.g., `.claude/worktrees/`), no special handling is needed — the main repo's CLAUDE.local.md is found automatically.

If CLAUDE.local.md already exists: read it, propose specific additions, and do not silently overwrite.

## Phase 6: Suggest and create skills (if user chose "Skills + hooks" or "Skills only")

Skills add capabilities Claude can use on demand without bloating every session.

**First, consume `skill` entries from the Phase 3 preference queue.** Each queued skill preference becomes a SKILL.md tailored to what the user described. For each:
- Name it from the preference (e.g., "verify-deep", "session-report", "deploy-sandbox")
- Write the body using the user's own words from the interview plus whatever Phase 2 found (test commands, report format, deploy target). If the preference maps to an existing bundled skill (e.g., `/verify`), write a project skill that adds the user's specific constraints on top — tell the user the bundled one still exists and theirs is additive.
- Ask a quick follow-up if the preference is underspecified (e.g., "which test command should verify-deep run?")

**Then suggest additional skills** beyond the queue when you find:
- Reference knowledge for specific tasks (conventions, patterns, style guides for a subsystem)
- Repeatable workflows the user would want to trigger directly (deploy, fix an issue, release process, verify changes)

For each suggested skill, provide: name, one-line purpose, and why it fits this repo.

If `.claude/skills/` already exists with skills, review them first. Do not overwrite existing skills — only propose new ones that complement what is already there.

Create each skill at `.claude/skills/<skill-name>/SKILL.md`:

```yaml
---
name: <skill-name>
description: <what the skill does and when to use it>
---

<Instructions for Claude>
```

Both the user (`/<skill-name>`) and Claude can invoke skills by default. For workflows with side effects (e.g., `/deploy`, `/fix-issue 123`), add `disable-model-invocation: true` so only the user can trigger it, and use `$ARGUMENTS` to accept input.

## Phase 7: Suggest additional optimizations

Tell the user you're going to suggest a few additional optimizations now that CLAUDE.md and skills (if chosen) are in place.

Check the environment and ask about each gap you find (use AskUserQuestion):

- **GitHub CLI**: Run `which gh` (or `where gh` on Windows). If it's missing AND the project uses GitHub (check `git remote -v` for github.com), ask the user if they want to install it. Explain that the GitHub CLI lets Claude help with commits, pull requests, issues, and code review directly.

- **Linting**: If Phase 2 found no lint config (no .eslintrc, ruff.toml, .golangci.yml, etc. for the project's language), ask the user if they want Claude to set up linting for this codebase. Explain that linting catches issues early and gives Claude fast feedback on its own edits.

- **Proposal-sourced hooks** (if user chose "Skills + hooks" or "Hooks only"): Consume `hook` entries from the Phase 3 preference queue. If Phase 2 found a formatter and the queue has no formatting hook, offer format-on-edit as a fallback. If the user chose "Neither" or "Skills only" in Phase 1, skip this bullet entirely.

  For each hook preference (from the queue or the formatter fallback):

  1. Target file: default based on the Phase 1 CLAUDE.md choice — project → `.claude/settings.json` (team-shared, committed); personal → `.claude/settings.local.json`. Only ask if the user chose "both" in Phase 1 or the preference is ambiguous. Ask once for all hooks, not per-hook.

  2. Pick the event and matcher from the preference:
     - "after every edit" → `PostToolUse` with matcher `Write|Edit`
     - "when Claude finishes" / "before I review" → `Stop` event (fires at the end of every turn — including read-only ones)
     - "before running bash" → `PreToolUse` with matcher `Bash`
     - "before committing" (literal git-commit gate) → **not a hooks.json hook.** Matchers can't filter Bash by command content, so there's no way to target only `git commit`. Route this to a git pre-commit hook (`.git/hooks/pre-commit`, husky, pre-commit framework) instead — offer to write one. If the user actually means "before I review and commit Claude's output", that's `Stop` — probe to disambiguate.
     Probe if the preference is ambiguous.

  3. **Load the hook reference** (once per `/init` run, before the first hook): invoke the Skill tool with `skill: 'update-config'` and args starting with `[hooks-only]` followed by a one-line summary of what you're building — e.g., `[hooks-only] Constructing a PostToolUse/Write|Edit format hook for .claude/settings.json using ruff`. This loads the hooks schema and verification flow into context. Subsequent hooks reuse it — don't re-invoke.

  4. Follow the skill's **"Constructing a Hook"** flow: dedup check → construct for THIS project → pipe-test raw → wrap → write JSON → `jq -e` validate → live-proof (for `Pre|PostToolUse` on triggerable matchers) → cleanup → handoff. Target file and event/matcher come from steps 1–2 above.

Act on each "yes" before moving on.

## Phase 8: Summary and next steps

Recap what was set up — which files were written and the key points included in each. Remind the user these files are a starting point: they should review and tweak them, and can run `/init` again anytime to re-scan.

Then tell the user that you'll be introducing a few more suggestions for optimizing their codebase and Claude Code setup based on what you found. Present these as a single, well-formatted to-do list where every item is relevant to this repo. Put the most impactful items first.

When building the list, work through these checks and include only what applies:
- If frontend code was detected (React, Vue, Svelte, etc.): `/plugin install frontend-design@claude-plugins-official` gives Claude design principles and component patterns so it produces polished UI; `/plugin install playwright@claude-plugins-official` lets Claude launch a real browser, screenshot what it built, and fix visual bugs itself.
- If you found gaps in Phase 7 (missing GitHub CLI, missing linting) and the user said no: list them here with a one-line reason why each helps.
- If tests are missing or sparse: suggest setting up a test framework so Claude can verify its own changes.
- To help you create skills and optimize existing skills using evals, Claude Code has an official skill-creator plugin you can install. Install it with `/plugin install skill-creator@claude-plugins-official`, then run `/skill-creator <skill-name>` to create new skills or refine any existing skill. (Always include this one.)
- Browse official plugins with `/plugin` — these bundle skills, agents, hooks, and MCP servers that you may find helpful. You can also create your own custom plugins to share them with others. (Always include this one.)
```
