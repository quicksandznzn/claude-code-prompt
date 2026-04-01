# buildCronCreatePrompt

- Source: `src/tools/ScheduleCronTool/prompt.ts`
- Symbol: `buildCronCreatePrompt`
- Line: 74
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Schedule a prompt to be enqueued at a future time. Use for both recurring schedules and one-shot reminders.

Uses standard 5-field cron in the user's local timezone: minute hour day-of-month month day-of-week. "0 9 * * *" means 9am local — no timezone conversion needed.

## One-shot tasks (recurring: false)

For "remind me at X" or "at <time>, do Y" requests — fire once then auto-delete.
Pin minute/hour/day-of-month/month to specific values:
  "remind me at 2:30pm today to check the deploy" → cron: "30 14 <today_dom> <today_month> *", recurring: false
  "tomorrow morning, run the smoke test" → cron: "57 8 <tomorrow_dom> <tomorrow_month> *", recurring: false

## Recurring jobs (recurring: true, the default)

For "every N minutes" / "every hour" / "weekdays at 9am" requests:
  "*/5 * * * *" (every 5 min), "0 * * * *" (hourly), "0 9 * * 1-5" (weekdays at 9am local)

## Avoid the :00 and :30 minute marks when the task allows it

Every user who asks for "9am" gets `0 9`, and every user who asks for "hourly" gets `0 *` — which means requests from across the planet land on the API at the same instant. When the user's request is approximate, pick a minute that is NOT 0 or 30:
  "every morning around 9" → "57 8 * * *" or "3 9 * * *" (not "0 9 * * *")
  "hourly" → "7 * * * *" (not "0 * * * *")
  "in an hour or so, remind me to..." → pick whatever minute you land on, don't round

Only use minute 0 or 30 when the user names that exact time and clearly means it ("at 9:00 sharp", "at half past", coordinating with a meeting). When in doubt, nudge a few minutes early or late — the user will not notice, and the fleet will.

${durabilitySection}

## Runtime behavior

Jobs only fire while the REPL is idle (not mid-query). ${durableRuntimeNote}The scheduler adds a small deterministic jitter on top of whatever you pick: recurring tasks fire up to 10% of their period late (max 15 min); one-shot tasks landing on :00 or :30 fire up to 90 s early. Picking an off-minute is still the bigger lever.

Recurring tasks auto-expire after ${DEFAULT_MAX_AGE_DAYS} days — they fire one final time, then are deleted. This bounds session lifetime. Tell the user about the ${DEFAULT_MAX_AGE_DAYS}-day limit when scheduling recurring jobs.

Returns a job ID you can pass to ${CRON_DELETE_TOOL_NAME}.
```

## Prompt Translation

```text
将一个提示词安排在未来某个时间入队。可用于周期性安排和一次性提醒。

使用用户本地时区的标准 5 字段 cron：minute hour day-of-month month day-of-week。"0 9 * * *" 表示本地时间上午 9 点，无需时区转换。

## 一次性任务（recurring: false）

对于“在 X 时提醒我”或“在 <time> 执行 Y”这类请求，触发一次后自动删除。
将 minute/hour/day-of-month/month 固定为具体值：
  “提醒我今天下午 2:30 检查部署” → cron: "30 14 <today_dom> <today_month> *", recurring: false
  “明天早上，运行冒烟测试” → cron: "57 8 <tomorrow_dom> <tomorrow_month> *", recurring: false

## 周期性任务（recurring: true，默认值）

对于“每 N 分钟”/“每小时”/“工作日早上 9 点”这类请求：
  "*/5 * * * *"（每 5 分钟一次），"0 * * * *"（每小时一次），"0 9 * * 1-5"（工作日当地时间上午 9 点）

## 在任务允许时，避免 :00 和 :30 这两个分钟标记

每个要求“上午 9 点”的用户都会得到 `0 9`，每个要求“每小时”的用户都会得到 `0 *`。这意味着来自全球的请求会在同一瞬间落到 API 上。如果用户的请求只是大致时间，请选择一个不是 0 或 30 的分钟：
  “每天早上 9 点左右” → "57 8 * * *" 或 "3 9 * * *"（不要用 "0 9 * * *"）
  “每小时” → "7 * * * *"（不要用 "0 * * * *"）
  “大约一小时后，提醒我……” → 选你落到的那个分钟值，不要四舍五入

只有在用户明确说出那个精确时间，并且显然就是那个意思时，才使用 minute 0 或 30（“9:00 整”、“半点”、“配合会议”）。拿不准时，就提前或延后几分钟，用户不会注意到，整个调度集群都会受益。

${durabilitySection}

## 运行时行为

任务只会在 REPL 空闲时触发（不会在查询进行中触发）。${durableRuntimeNote}调度器会在你选择的时间上叠加一点小的确定性抖动：周期性任务最迟会比周期晚 10% 触发，最多 15 分钟；落在 :00 或 :30 的一次性任务会最多提前 90 秒触发。选择非 0 或 30 的分钟仍然是更关键的调节手段。

周期性任务会在 ${DEFAULT_MAX_AGE_DAYS} 天后自动过期。它们会最后再触发一次，然后被删除。这样可以限制会话生命周期。安排周期性任务时，要向用户说明这个 ${DEFAULT_MAX_AGE_DAYS} 天限制。

返回一个任务 ID，你可以将其传给 ${CRON_DELETE_TOOL_NAME}。
```
