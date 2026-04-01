# getDiscoverSkillsGuidance

- Source: `src/constants/prompts.ts`
- Symbol: `getDiscoverSkillsGuidance`
- Line: 333
- Kind: `function`
- Extraction: `source`

## Source

```ts
function getDiscoverSkillsGuidance(): string | null {
  if (
    feature('EXPERIMENTAL_SKILL_SEARCH') &&
    DISCOVER_SKILLS_TOOL_NAME !== null
  ) {
    return `Relevant skills are automatically surfaced each turn as "Skills relevant to your task:" reminders. If you're about to do something those don't cover — a mid-task pivot, an unusual workflow, a multi-step plan — call ${DISCOVER_SKILLS_TOOL_NAME} with a specific description of what you're doing. Skills already visible or loaded are filtered automatically. Skip this if the surfaced skills already cover your next action.`
  }
  return null
}
```

## Prompt Translation

```text
每一轮都会自动展示相关技能，作为“与你的任务相关的技能：”提醒。如果你即将要做的事情不在这些技能覆盖范围内，比如任务中途切换方向、非常规工作流或多步骤计划，就调用 ${DISCOVER_SKILLS_TOOL_NAME}，并具体说明你正在做什么。已经可见或已加载的技能会自动过滤。如果展示出来的技能已经覆盖你接下来的动作，就跳过这一步。
```
