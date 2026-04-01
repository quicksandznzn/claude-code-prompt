# ASK_USER_QUESTION_TOOL_PROMPT

- Source: `src/tools/AskUserQuestionTool/prompt.ts`
- Symbol: `ASK_USER_QUESTION_TOOL_PROMPT`
- Line: 32
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Use this tool when you need to ask the user questions during execution. This allows you to:
1. Gather user preferences or requirements
2. Clarify ambiguous instructions
3. Get decisions on implementation choices as you work
4. Offer choices to the user about what direction to take.

Usage notes:
- Users will always be able to select "Other" to provide custom text input
- Use multiSelect: true to allow multiple answers to be selected for a question
- If you recommend a specific option, make that the first option in the list and add "(Recommended)" at the end of the label

Plan mode note: In plan mode, use this tool to clarify requirements or choose between approaches BEFORE finalizing your plan. Do NOT use this tool to ask "Is my plan ready?" or "Should I proceed?" - use ${EXIT_PLAN_MODE_TOOL_NAME} for plan approval. IMPORTANT: Do not reference "the plan" in your questions (e.g., "Do you have feedback about the plan?", "Does the plan look good?") because the user cannot see the plan in the UI until you call ${EXIT_PLAN_MODE_TOOL_NAME}. If you need plan approval, use ${EXIT_PLAN_MODE_TOOL_NAME} instead.
```

## Prompt Translation

```text
在执行过程中需要向用户提问时使用此工具。这样你可以：
1. 收集用户偏好或需求
2. 澄清有歧义的指令
3. 在工作过程中就实现选择征求决策
4. 向用户提供可选方向，帮助决定下一步怎么走。

使用说明：
- 用户始终可以选择 "Other" 来提供自定义文本输入
- 使用 `multiSelect: true` 允许对某个问题选择多个答案
- 如果你推荐某个特定选项，请把它放在列表的第一项，并在标签末尾加上 "(Recommended)"

计划模式说明：在计划模式下，请在最终确定计划之前使用此工具来澄清需求或在不同方案之间做出选择。不要使用此工具询问“我的计划准备好了吗？”或“我应该继续吗？” - 计划审批请使用 ${EXIT_PLAN_MODE_TOOL_NAME}。重要：不要在问题中提到“计划”（例如：“你对计划有什么反馈吗？”，“这个计划看起来好吗？”），因为在你调用 ${EXIT_PLAN_MODE_TOOL_NAME} 之前，用户在 UI 中看不到计划。如果你需要计划审批，请改用 ${EXIT_PLAN_MODE_TOOL_NAME}。
```
