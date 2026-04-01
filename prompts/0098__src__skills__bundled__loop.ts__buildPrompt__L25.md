# buildPrompt

- Source: `src/skills/bundled/loop.ts`
- Symbol: `buildPrompt`
- Line: 25
- Kind: `function`
- Extraction: `text`

## Prompt

```text
# /loop — schedule a recurring prompt

Parse the input below into `[interval] <prompt…>` and schedule it with ${CRON_CREATE_TOOL_NAME}.

## Parsing (in priority order)

1. **Leading token**: if the first whitespace-delimited token matches `^\d+[smhd]$` (e.g. `5m`, `2h`), that's the interval; the rest is the prompt.
2. **Trailing "every" clause**: otherwise, if the input ends with `every <N><unit>` or `every <N> <unit-word>` (e.g. `every 20m`, `every 5 minutes`, `every 2 hours`), extract that as the interval and strip it from the prompt. Only match when what follows "every" is a time expression — `check every PR` has no interval.
3. **Default**: otherwise, interval is `${DEFAULT_INTERVAL}` and the entire input is the prompt.

If the resulting prompt is empty, show usage `/loop [interval] <prompt>` and stop — do not call ${CRON_CREATE_TOOL_NAME}.

Examples:
- `5m /babysit-prs` → interval `5m`, prompt `/babysit-prs` (rule 1)
- `check the deploy every 20m` → interval `20m`, prompt `check the deploy` (rule 2)
- `run tests every 5 minutes` → interval `5m`, prompt `run tests` (rule 2)
- `check the deploy` → interval `${DEFAULT_INTERVAL}`, prompt `check the deploy` (rule 3)
- `check every PR` → interval `${DEFAULT_INTERVAL}`, prompt `check every PR` (rule 3 — "every" not followed by time)
- `5m` → empty prompt → show usage

## Interval → cron

Supported suffixes: `s` (seconds, rounded up to nearest minute, min 1), `m` (minutes), `h` (hours), `d` (days). Convert:

| Interval pattern      | Cron expression     | Notes                                    |
|-----------------------|---------------------|------------------------------------------|
| `Nm` where N ≤ 59   | `*/N * * * *`     | every N minutes                          |
| `Nm` where N ≥ 60   | `0 */H * * *`     | round to hours (H = N/60, must divide 24)|
| `Nh` where N ≤ 23   | `0 */N * * *`     | every N hours                            |
| `Nd`                | `0 0 */N * *`     | every N days at midnight local           |
| `Ns`                | treat as `ceil(N/60)m` | cron minimum granularity is 1 minute  |

**If the interval doesn't cleanly divide its unit** (e.g. `7m` → `*/7 * * * *` gives uneven gaps at :56→:00; `90m` → 1.5h which cron can't express), pick the nearest clean interval and tell the user what you rounded to before scheduling.

## Action

1. Call ${CRON_CREATE_TOOL_NAME} with:
   - `cron`: the expression from the table above
   - `prompt`: the parsed prompt from above, verbatim (slash commands are passed through unchanged)
   - `recurring`: `true`
2. Briefly confirm: what's scheduled, the cron expression, the human-readable cadence, that recurring tasks auto-expire after ${DEFAULT_MAX_AGE_DAYS} days, and that they can cancel sooner with ${CRON_DELETE_TOOL_NAME} (include the job ID).
3. **Then immediately execute the parsed prompt now** — don't wait for the first cron fire. If it's a slash command, invoke it via the Skill tool; otherwise act on it directly.

## Input

${args}
```

## Prompt Translation

```text
# /loop — 计划一个定期提示词

将下面的输入解析为 `[interval] <prompt…>`，并通过 ${CRON_CREATE_TOOL_NAME} 来安排它。

## 解析（按优先级顺序）

1. **首个 token**：如果第一个以空白分隔的 token 匹配 `^\d+[smhd]$`（例如 `5m`、`2h`），那它就是间隔；其余部分是提示词。
2. **末尾的 "every" 短语**：否则，如果输入以 `every <N><unit>` 或 `every <N> <unit-word>` 结尾（例如 `every 20m`、`every 5 minutes`、`every 2 hours`），就把这一段提取为间隔，并从提示词中去掉。只有当 "every" 后面跟的是时间表达式时才匹配 — `check every PR` 没有间隔。
3. **默认**：否则，间隔为 `${DEFAULT_INTERVAL}`，整个输入都是提示词。

如果最终得到的提示词为空，显示用法 `/loop [interval] <prompt>` 并停止 — 不要调用 ${CRON_CREATE_TOOL_NAME}。

示例：
- `5m /babysit-prs` → 间隔 `5m`，提示词 `/babysit-prs`（规则 1）
- `check the deploy every 20m` → 间隔 `20m`，提示词 `check the deploy`（规则 2）
- `run tests every 5 minutes` → 间隔 `5m`，提示词 `run tests`（规则 2）
- `check the deploy` → 间隔 `${DEFAULT_INTERVAL}`，提示词 `check the deploy`（规则 3）
- `check every PR` → 间隔 `${DEFAULT_INTERVAL}`，提示词 `check every PR`（规则 3 — "every" 后面不是时间表达式）
- `5m` → 提示词为空 → 显示用法

## 间隔 → cron

支持的后缀：`s`（秒，向上取整到最近的分钟，最少按 1 分钟处理）、`m`（分钟）、`h`（小时）、`d`（天）。转换如下：

| 间隔模式           | Cron 表达式         | 说明                                     |
|--------------------|----------------------|------------------------------------------|
| `Nm`（N ≤ 59）     | `*/N * * * *`        | 每 N 分钟一次                             |
| `Nm`（N ≥ 60）     | `0 */H * * *`        | 折算成小时（H = N/60，必须能整除 24）      |
| `Nh`（N ≤ 23）     | `0 */N * * *`        | 每 N 小时一次                             |
| `Nd`               | `0 0 */N * *`        | 每 N 天一次，在本地午夜执行                |
| `Ns`               | 视为 `ceil(N/60)m`   | cron 的最小粒度是 1 分钟                  |

**如果该间隔无法整齐地表示成其单位的整数倍**（例如 `7m` → `*/7 * * * *` 会在 :56→:00 处出现不均匀间隔；`90m` → 1.5h，而 cron 无法表达），请选择最接近的整洁间隔，并在调度前告诉用户你把它四舍五入到了什么。

## 动作

1. 使用以下参数调用 ${CRON_CREATE_TOOL_NAME}：
   - `cron`：上表中的表达式
   - `prompt`：上面解析出的提示词，逐字原样传入（斜杠命令会原样传递）
   - `recurring`：`true`
2. 简要确认：安排了什么、cron 表达式、人类可读的执行频率、这些循环任务会在 ${DEFAULT_MAX_AGE_DAYS} 天后自动过期，以及可以通过 ${CRON_DELETE_TOOL_NAME} 更早取消（包含作业 ID）。
3. **然后立即执行刚解析出的提示词** — 不要等到第一次 cron 触发。如果它是斜杠命令，就通过 Skill 工具调用；否则直接执行它。

## 输入

${args}
```
