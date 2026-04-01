# INSIGHT_SECTIONS.prompt

- Source: `src/commands/insights.ts`
- Symbol: `INSIGHT_SECTIONS.prompt`
- Line: 1394
- Kind: `property`
- Extraction: `text`

## Prompt

```text
Analyze this Claude Code usage data and suggest improvements.

## CC FEATURES REFERENCE (pick from these for features_to_try):
1. **MCP Servers**: Connect Claude to external tools, databases, and APIs via Model Context Protocol.
   - How to use: Run `claude mcp add <server-name> -- <command>`
   - Good for: database queries, Slack integration, GitHub issue lookup, connecting to internal APIs

2. **Custom Skills**: Reusable prompts you define as markdown files that run with a single /command.
   - How to use: Create `.claude/skills/commit/SKILL.md` with instructions. Then type `/commit` to run it.
   - Good for: repetitive workflows - /commit, /review, /test, /deploy, /pr, or complex multi-step workflows

3. **Hooks**: Shell commands that auto-run at specific lifecycle events.
   - How to use: Add to `.claude/settings.json` under "hooks" key.
   - Good for: auto-formatting code, running type checks, enforcing conventions

4. **Headless Mode**: Run Claude non-interactively from scripts and CI/CD.
   - How to use: `claude -p "fix lint errors" --allowedTools "Edit,Read,Bash"`
   - Good for: CI/CD integration, batch code fixes, automated reviews

5. **Task Agents**: Claude spawns focused sub-agents for complex exploration or parallel work.
   - How to use: Claude auto-invokes when helpful, or ask "use an agent to explore X"
   - Good for: codebase exploration, understanding complex systems

RESPOND WITH ONLY A VALID JSON OBJECT:
{
  "claude_md_additions": [
    {"addition": "A specific line or block to add to CLAUDE.md based on workflow patterns. E.g., 'Always run tests after modifying auth-related files'", "why": "1 sentence explaining why this would help based on actual sessions", "prompt_scaffold": "Instructions for where to add this in CLAUDE.md. E.g., 'Add under ## Testing section'"}
  ],
  "features_to_try": [
    {"feature": "Feature name from CC FEATURES REFERENCE above", "one_liner": "What it does", "why_for_you": "Why this would help YOU based on your sessions", "example_code": "Actual command or config to copy"}
  ],
  "usage_patterns": [
    {"title": "Short title", "suggestion": "1-2 sentence summary", "detail": "3-4 sentences explaining how this applies to YOUR work", "copyable_prompt": "A specific prompt to copy and try"}
  ]
}

IMPORTANT for claude_md_additions: PRIORITIZE instructions that appear MULTIPLE TIMES in the user data. If user told Claude the same thing in 2+ sessions (e.g., 'always run tests', 'use TypeScript'), that's a PRIME candidate - they shouldn't have to repeat themselves.

IMPORTANT for features_to_try: Pick 2-3 from the CC FEATURES REFERENCE above. Include 2-3 items for each category.
```

## Prompt Translation

```text
分析这份 Claude Code 使用数据并提出改进建议。

## CC 功能参考（在 features_to_try 中从这些内容里选择）：
1. **MCP 服务器**：通过模型上下文协议将 Claude 连接到外部工具、数据库和 API。
   - 用法：运行 `claude mcp add <server-name> -- <command>`
   - 适合：数据库查询、Slack 集成、GitHub issue 查询、连接内部 API

2. **自定义技能**：你定义的可复用提示词，以 markdown 文件形式存在，只需一个 /command 就能运行。
   - 用法：创建 `.claude/skills/commit/SKILL.md` 并写入说明。然后输入 `/commit` 来运行它。
   - 适合：重复性工作流 - /commit、/review、/test、/deploy、/pr，或复杂的多步骤工作流

3. **Hooks**：会在特定生命周期事件自动运行的 shell 命令。
   - 用法：添加到 `.claude/settings.json` 的 "hooks" 键下。
   - 适合：自动格式化代码、运行类型检查、强制执行约定

4. **无头模式**：从脚本和 CI/CD 中以非交互方式运行 Claude。
   - 用法：`claude -p "fix lint errors" --allowedTools "Edit,Read,Bash"`
   - 适合：CI/CD 集成、批量修复代码、自动化审查

5. **任务代理**：Claude 会为复杂探索或并行工作生成专注的子代理。
   - 用法：在有帮助时 Claude 会自动调用，或者你可以要求“用一个代理来探索 X”
   - 适合：代码库探索、理解复杂系统

只返回一个有效的 JSON 对象：
{
  "claude_md_additions": [
    {"addition": "根据工作流模式，添加一行或一段到 CLAUDE.md 中。例如：'始终在修改认证相关文件后运行测试'", "why": "用真实会话中的信息解释这条内容为什么有帮助的一句话", "prompt_scaffold": "说明应将其添加到 CLAUDE.md 的什么位置。例如：'添加到 ## 测试 部分下'"}
  ],
  "features_to_try": [
    {"feature": "来自上方 CC 功能参考的功能名称", "one_liner": "它的作用", "why_for_you": "基于你的会话，这为什么会对你有帮助", "example_code": "可直接复制的实际命令或配置"}
  ],
  "usage_patterns": [
    {"title": "简短标题", "suggestion": "1-2 句总结建议", "detail": "3-4 句说明这如何适用于你的工作", "copyable_prompt": "一个可以直接复制并尝试的具体提示词"}
  ]
}

重要：对于 claude_md_additions：优先选择在用户数据中多次出现的指令。如果用户在 2 次及以上会话里对 Claude 说过同一件事（例如“始终运行测试”、“使用 TypeScript”），那就是首要候选 - 他们不应该反复重复这些要求。

重要：对于 features_to_try：从上方的 CC 功能参考中选择 2-3 个。每个类别包含 2-3 项。
```
