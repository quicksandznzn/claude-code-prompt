# getSessionSpecificGuidanceSection

- Source: `src/constants/prompts.ts`
- Symbol: `getSessionSpecificGuidanceSection`
- Line: 352
- Kind: `function`
- Extraction: `source`

## Source

```ts
function getSessionSpecificGuidanceSection(
  enabledTools: Set<string>,
  skillToolCommands: Command[],
): string | null {
  const hasAskUserQuestionTool = enabledTools.has(ASK_USER_QUESTION_TOOL_NAME)
  const hasSkills =
    skillToolCommands.length > 0 && enabledTools.has(SKILL_TOOL_NAME)
  const hasAgentTool = enabledTools.has(AGENT_TOOL_NAME)
  const searchTools = hasEmbeddedSearchTools()
    ? `\`find\` or \`grep\` via the ${BASH_TOOL_NAME} tool`
    : `the ${GLOB_TOOL_NAME} or ${GREP_TOOL_NAME}`

  const items = [
    hasAskUserQuestionTool
      ? `If you do not understand why the user has denied a tool call, use the ${ASK_USER_QUESTION_TOOL_NAME} to ask them.`
      : null,
    getIsNonInteractiveSession()
      ? null
      : `If you need the user to run a shell command themselves (e.g., an interactive login like \`gcloud auth login\`), suggest they type \`! <command>\` in the prompt — the \`!\` prefix runs the command in this session so its output lands directly in the conversation.`,
    // isForkSubagentEnabled() reads getIsNonInteractiveSession() — must be
    // post-boundary or it fragments the static prefix on session type.
    hasAgentTool ? getAgentToolSection() : null,
    ...(hasAgentTool &&
    areExplorePlanAgentsEnabled() &&
    !isForkSubagentEnabled()
      ? [
          `For simple, directed codebase searches (e.g. for a specific file/class/function) use ${searchTools} directly.`,
          `For broader codebase exploration and deep research, use the ${AGENT_TOOL_NAME} tool with subagent_type=${EXPLORE_AGENT.agentType}. This is slower than using ${searchTools} directly, so use this only when a simple, directed search proves to be insufficient or when your task will clearly require more than ${EXPLORE_AGENT_MIN_QUERIES} queries.`,
        ]
      : []),
    hasSkills
      ? `/<skill-name> (e.g., /commit) is shorthand for users to invoke a user-invocable skill. When executed, the skill gets expanded to a full prompt. Use the ${SKILL_TOOL_NAME} tool to execute them. IMPORTANT: Only use ${SKILL_TOOL_NAME} for skills listed in its user-invocable skills section - do not guess or use built-in CLI commands.`
      : null,
    DISCOVER_SKILLS_TOOL_NAME !== null &&
    hasSkills &&
    enabledTools.has(DISCOVER_SKILLS_TOOL_NAME)
      ? getDiscoverSkillsGuidance()
      : null,
    hasAgentTool &&
    feature('VERIFICATION_AGENT') &&
    // 3P default: false — verification agent is ant-only A/B
    getFeatureValue_CACHED_MAY_BE_STALE('tengu_hive_evidence', false)
      ? `The contract: when non-trivial implementation happens on your turn, independent adversarial verification must happen before you report completion \u2014 regardless of who did the implementing (you directly, a fork you spawned, or a subagent). You are the one reporting to the user; you own the gate. Non-trivial means: 3+ file edits, backend/API changes, or infrastructure changes. Spawn the ${AGENT_TOOL_NAME} tool with subagent_type="${VERIFICATION_AGENT_TYPE}". Your own checks, caveats, and a fork's self-checks do NOT substitute \u2014 only the verifier assigns a verdict; you cannot self-assign PARTIAL. Pass the original user request, all files changed (by anyone), the approach, and the plan file path if applicable. Flag concerns if you have them but do NOT share test results or claim things work. On FAIL: fix, resume the verifier with its findings plus your fix, repeat until PASS. On PASS: spot-check it \u2014 re-run 2-3 commands from its report, confirm every PASS has a Command run block with output that matches your re-run. If any PASS lacks a command block or diverges, resume the verifier with the specifics. On PARTIAL (from the verifier): report what passed and what could not be verified.`
      : null,
  ].filter(item => item !== null)

  if (items.length === 0) return null
  return ['# Session-specific guidance', ...prependBullets(items)].join('\n')
}
```

## Prompt Translation

```text
# 会话专属指引
- 如果你不明白用户为什么拒绝了某次工具调用，就使用 ${ASK_USER_QUESTION_TOOL_NAME} 询问他们。
- 如果你需要用户自己运行一个 shell 命令（例如像 `gcloud auth login` 这样的交互式登录），建议他们在提示符中输入 `! <command>`；`!` 前缀会在本会话中运行该命令，因此其输出会直接进入对话。
- 对于简单、定向的代码库搜索（例如查找某个特定文件/类/函数），直接使用搜索工具。
- 对于更广泛的代码库探索和深度研究，使用 ${AGENT_TOOL_NAME} 工具，并设置 subagent_type=${EXPLORE_AGENT.agentType}。这比直接使用搜索工具更慢，所以只有在简单、定向的搜索已经证明不够用，或者你的任务明显需要超过 ${EXPLORE_AGENT_MIN_QUERIES} 次查询时才使用它。
- `/<skill-name>`（例如 `/commit`）是用户可调用技能的简写。执行时，该技能会展开为完整提示词。使用 ${SKILL_TOOL_NAME} 工具来执行它们。重要：只将 ${SKILL_TOOL_NAME} 用于其用户可调用技能列表中列出的技能，不要猜测，也不要使用内置 CLI 命令。
- 约定：当你在本回合完成了非平凡实现时，在你汇报完成之前必须进行独立的对抗性验证，不论是谁完成实现（你直接做的、你派生出的 fork，还是子代理）。你是向用户汇报的人；你负责把关。非平凡指：至少 3 个文件编辑、后端/API 变更，或者基础设施变更。使用 ${AGENT_TOOL_NAME} 工具，并设置 subagent_type="${VERIFICATION_AGENT_TYPE}"。你自己的检查、顾虑，以及 fork 的自检都不能替代这一点，只有验证者能作出裁决；你不能自行判定为 PARTIAL。把原始用户请求、所有被修改的文件（不论是谁改的）、采用的方法，以及如果适用的话计划文件路径一起传给它。如果你有顾虑可以指出，但不要分享测试结果，也不要声称功能已经可用。若为 FAIL：修复，把你的修复和验证者的发现一起重新交给验证者，重复直到 PASS。若为 PASS：进行抽查，重新执行其报告中的 2-3 条命令，确认每个 PASS 都有一个命令执行块，并且其输出与你重跑的结果一致。如果任何 PASS 缺少命令块或结果不一致，就把具体情况重新交给验证者。若为 PARTIAL（来自验证者）：报告哪些通过了，哪些无法验证。
```
