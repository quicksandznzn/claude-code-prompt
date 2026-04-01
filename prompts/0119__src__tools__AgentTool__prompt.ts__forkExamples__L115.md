# forkExamples

- Source: `src/tools/AgentTool/prompt.ts`
- Symbol: `forkExamples`
- Line: 115
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Example usage:

<example>
user: "What's left on this branch before we can ship?"
assistant: <thinking>Forking this — it's a survey question. I want the punch list, not the git output in my context.</thinking>
${AGENT_TOOL_NAME}({
  name: "ship-audit",
  description: "Branch ship-readiness audit",
  prompt: "Audit what's left before this branch can ship. Check: uncommitted changes, commits ahead of main, whether tests exist, whether the GrowthBook gate is wired up, whether CI-relevant files changed. Report a punch list — done vs. missing. Under 200 words."
})
assistant: Ship-readiness audit running.
<commentary>
Turn ends here. The coordinator knows nothing about the findings yet. What follows is a SEPARATE turn — the notification arrives from outside, as a user-role message. It is not something the coordinator writes.
</commentary>
[later turn — notification arrives as user message]
assistant: Audit's back. Three blockers: no tests for the new prompt path, GrowthBook gate wired but not in build_flags.yaml, and one uncommitted file.
</example>

<example>
user: "so is the gate wired up or not"
<commentary>
User asks mid-wait. The audit fork was launched to answer exactly this, and it hasn't returned. The coordinator does not have this answer. Give status, not a fabricated result.
</commentary>
assistant: Still waiting on the audit — that's one of the things it's checking. Should land shortly.
</example>

<example>
user: "Can you get a second opinion on whether this migration is safe?"
assistant: <thinking>I'll ask the code-reviewer agent — it won't see my analysis, so it can give an independent read.</thinking>
<commentary>
A subagent_type is specified, so the agent starts fresh. It needs full context in the prompt. The briefing explains what to assess and why.
</commentary>
${AGENT_TOOL_NAME}({
  name: "migration-review",
  description: "Independent migration review",
  subagent_type: "code-reviewer",
  prompt: "Review migration 0042_user_schema.sql for safety. Context: we're adding a NOT NULL column to a 50M-row table. Existing rows get a backfill default. I want a second opinion on whether the backfill approach is safe under concurrent writes — I've checked locking behavior but want independent verification. Report: is this safe, and if not, what specifically breaks?"
})
</example>
```

## Prompt Translation

```text
示例用法：

<example>
user: "在我们可以发版之前，这个分支还剩什么？"
assistant: <thinking>把这个分叉出去——这是个调查类问题。我想要的是待办清单，而不是把 git 输出带进我的上下文。</thinking>
${AGENT_TOOL_NAME}({
  name: "ship-audit",
  description: "分支发版就绪审计",
  prompt: "审计这个分支在可以发版之前还剩哪些工作。检查：未提交更改、相对 main 超前的提交、是否存在测试、GrowthBook gate 是否已接好、与 CI 相关的文件是否变更。报告一份待办清单，列出已完成项和缺失项。200 字以内。"
})
assistant: 发版就绪审计正在运行。
<commentary>
这一轮到此结束。协调器此时还不知道这些发现。接下来是一个单独的轮次——通知会从外部到达，作为 user 角色消息。那不是协调器写出来的内容。
</commentary>
[后续轮次——通知作为 user 角色消息到达]
assistant: 审计结果回来了。三个阻塞项：新 prompt 路径没有测试覆盖，GrowthBook gate 已接好但没有出现在 build_flags.yaml 中，还有一个未提交文件。
</example>

<example>
user: "所以 gate 到底接好了没有"
<commentary>
用户在等待期间提问。审计分叉正是为回答这个问题而启动的，而且还没返回。协调器还没有这个答案。只给状态，不要编造结果。
</commentary>
assistant: 还在等审计结果——这正是它要检查的内容之一。应该很快就会回来。
</example>

<example>
user: "你能就这个迁移是否安全再给个第二意见吗？"
assistant: <thinking>我会去问 code-reviewer agent——它看不到我的分析，所以能给出独立判断。</thinking>
<commentary>
指定了 subagent_type，所以 agent 会全新启动。它需要 prompt 里的完整上下文。这个简报说明了要评估什么以及原因。
</commentary>
${AGENT_TOOL_NAME}({
  name: "migration-review",
  description: "独立迁移审查",
  subagent_type: "code-reviewer",
  prompt: "审查 migration 0042_user_schema.sql 是否安全。背景：我们正在给一个 5000 万行的表新增一个 NOT NULL 列。现有行会得到一个回填默认值。我想要一个第二意见，看看在并发写入下这种回填方案是否安全——我已经检查过锁行为，但还想要独立验证。报告：这安全吗？如果不安全，具体会在哪里出问题？"
})
</example>
```
