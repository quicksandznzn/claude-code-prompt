# SKILL_PROMPT

- Source: `src/skills/bundled/remember.ts`
- Symbol: `SKILL_PROMPT`
- Line: 9
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
# Memory Review

## Goal
Review the user's memory landscape and produce a clear report of proposed changes, grouped by action type. Do NOT apply changes — present proposals for user approval.

## Steps

### 1. Gather all memory layers
Read CLAUDE.md and CLAUDE.local.md from the project root (if they exist). Your auto-memory content is already in your system prompt — review it there. Note which team memory sections exist, if any.

**Success criteria**: You have the contents of all memory layers and can compare them.

### 2. Classify each auto-memory entry
For each substantive entry in auto-memory, determine the best destination:

| Destination | What belongs there | Examples |
|---|---|---|
| **CLAUDE.md** | Project conventions and instructions for Claude that all contributors should follow | "use bun not npm", "API routes use kebab-case", "test command is bun test", "prefer functional style" |
| **CLAUDE.local.md** | Personal instructions for Claude specific to this user, not applicable to other contributors | "I prefer concise responses", "always explain trade-offs", "don't auto-commit", "run tests before committing" |
| **Team memory** | Org-wide knowledge that applies across repositories (only if team memory is configured) | "deploy PRs go through #deploy-queue", "staging is at staging.internal", "platform team owns infra" |
| **Stay in auto-memory** | Working notes, temporary context, or entries that don't clearly fit elsewhere | Session-specific observations, uncertain patterns |

**Important distinctions:**
- CLAUDE.md and CLAUDE.local.md contain instructions for Claude, not user preferences for external tools (editor theme, IDE keybindings, etc. don't belong in either)
- Workflow practices (PR conventions, merge strategies, branch naming) are ambiguous — ask the user whether they're personal or team-wide
- When unsure, ask rather than guess

**Success criteria**: Each entry has a proposed destination or is flagged as ambiguous.

### 3. Identify cleanup opportunities
Scan across all layers for:
- **Duplicates**: Auto-memory entries already captured in CLAUDE.md or CLAUDE.local.md → propose removing from auto-memory
- **Outdated**: CLAUDE.md or CLAUDE.local.md entries contradicted by newer auto-memory entries → propose updating the older layer
- **Conflicts**: Contradictions between any two layers → propose resolution, noting which is more recent

**Success criteria**: All cross-layer issues identified.

### 4. Present the report
Output a structured report grouped by action type:
1. **Promotions** — entries to move, with destination and rationale
2. **Cleanup** — duplicates, outdated entries, conflicts to resolve
3. **Ambiguous** — entries where you need the user's input on destination
4. **No action needed** — brief note on entries that should stay put

If auto-memory is empty, say so and offer to review CLAUDE.md for cleanup.

**Success criteria**: User can review and approve/reject each proposal individually.

## Rules
- Present ALL proposals before making any changes
- Do NOT modify files without explicit user approval
- Do NOT create new files unless the target doesn't exist yet
- Ask about ambiguous entries — don't guess
```

## Prompt Translation

```text
# 记忆审查

## 目标
审查用户的记忆层，按行动类型分组，生成一份清晰的拟议更改报告。不要应用更改——只呈现提案供用户批准。

## 步骤

### 1. 收集所有记忆层
从项目根目录读取 CLAUDE.md 和 CLAUDE.local.md（如果它们存在）。你的自动记忆内容已经在系统提示中——请在那里审查它。注明有哪些团队记忆部分（如果有）。

**成功标准**：你已获得所有记忆层的内容，并且可以对它们进行比较。

### 2. 对每一条自动记忆进行分类
对于自动记忆中的每一条实质性条目，确定最佳归属位置：

| 归属位置 | 适合放在这里的内容 | 示例 |
|---|---|---|
| **CLAUDE.md** | 项目规范以及所有贡献者都应遵循的 Claude 指令 | "使用 bun，不要用 npm", "API 路由使用 kebab-case", "测试命令是 bun test", "偏好函数式风格" |
| **CLAUDE.local.md** | 仅适用于该用户、与其他贡献者无关的 Claude 个人指令 | "我偏好简洁回复", "始终说明权衡", "不要自动提交", "提交前运行测试" |
| **团队记忆** | 跨仓库适用的组织级知识（仅在已配置团队记忆时） | "发布 PR 通过 #deploy-queue", "staging 在 staging.internal", "platform 团队负责基础设施" |
| **保留在自动记忆中** | 工作笔记、临时上下文，或不明确适合其他位置的条目 | 本次会话中的观察、不确定的模式 |

**重要区别：**
- CLAUDE.md 和 CLAUDE.local.md 包含的是给 Claude 的指令，而不是给外部工具的用户偏好（编辑器主题、IDE 快捷键等不属于这两者）
- 工作流实践（PR 约定、合并策略、分支命名）有歧义——请询问用户它们是个人级还是团队级
- 不确定时，先询问，不要猜测

**成功标准**：每条条目都有一个建议归属，或者被标记为歧义。

### 3. 识别清理机会
在所有层之间扫描以下内容：
- **重复项**：已经收录在 CLAUDE.md 或 CLAUDE.local.md 中的自动记忆条目 → 建议从自动记忆中移除
- **过时项**：被更新的自动记忆条目所推翻的 CLAUDE.md 或 CLAUDE.local.md 条目 → 建议更新较旧的层
- **冲突项**：任意两个层之间的矛盾 → 建议解决，并注明哪一条更新

**成功标准**：已识别所有跨层问题。

### 4. 呈现报告
输出一份按行动类型分组的结构化报告：
1. **晋升** — 要移动的条目，包含目标位置和理由
2. **清理** — 重复项、过时项、需要解决的冲突
3. **歧义项** — 需要用户就归属位置提供意见的条目
4. **无需处理** — 简要说明应保持原状的条目

如果自动记忆为空，请说明这一点，并提议审查 CLAUDE.md 以进行清理。

**成功标准**：用户可以逐项审查并批准或拒绝每一项提案。

## 规则
- 在做出任何更改之前，先呈现所有提案
- 未经用户明确批准，不要修改文件
- 不要创建新文件，除非目标文件尚不存在
- 对歧义条目要询问用户，不要猜测
```
