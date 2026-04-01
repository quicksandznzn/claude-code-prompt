# FACET_EXTRACTION_PROMPT

- Source: `src/commands/insights.ts`
- Symbol: `FACET_EXTRACTION_PROMPT`
- Line: 430
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Analyze this Claude Code session and extract structured facets.

CRITICAL GUIDELINES:

1. **goal_categories**: Count ONLY what the USER explicitly asked for.
   - DO NOT count Claude's autonomous codebase exploration
   - DO NOT count work Claude decided to do on its own
   - ONLY count when user says "can you...", "please...", "I need...", "let's..."

2. **user_satisfaction_counts**: Base ONLY on explicit user signals.
   - "Yay!", "great!", "perfect!" → happy
   - "thanks", "looks good", "that works" → satisfied
   - "ok, now let's..." (continuing without complaint) → likely_satisfied
   - "that's not right", "try again" → dissatisfied
   - "this is broken", "I give up" → frustrated

3. **friction_counts**: Be specific about what went wrong.
   - misunderstood_request: Claude interpreted incorrectly
   - wrong_approach: Right goal, wrong solution method
   - buggy_code: Code didn't work correctly
   - user_rejected_action: User said no/stop to a tool call
   - excessive_changes: Over-engineered or changed too much

4. If very short or just warmup, use warmup_minimal for goal_category

SESSION:
```

## Prompt Translation

```text
分析这段 Claude Code 会话并提取结构化要素。

关键准则：

1. **goal_categories**：只统计用户明确要求的内容。
   - 不要统计 Claude 自主进行的代码库探索
   - 不要统计 Claude 自己决定去做的工作
   - 只有当用户说“can you...”、“please...”、“I need...”、“let's...”时才计数

2. **user_satisfaction_counts**：只根据用户明确表达的信号判断。
   - “Yay!”、“great!”、“perfect!” → happy
   - “thanks”、“looks good”、“that works” → satisfied
   - “ok, now let's...” （在没有抱怨的情况下继续）→ likely_satisfied
   - “that's not right”、“try again” → dissatisfied
   - “this is broken”、“I give up” → frustrated

3. **friction_counts**：要具体说明哪里出了问题。
   - misunderstood_request：Claude 误解了请求
   - wrong_approach：目标正确，但解决方法不对
   - buggy_code：代码没有正常工作
   - user_rejected_action：用户对某个工具调用说了不/停止
   - excessive_changes：过度设计或改动过多

4. 如果内容非常短，或者只是热身，则将 goal_category 设为 warmup_minimal

会话：
```
