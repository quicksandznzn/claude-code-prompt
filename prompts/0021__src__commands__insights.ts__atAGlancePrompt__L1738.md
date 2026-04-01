# atAGlancePrompt

- Source: `src/commands/insights.ts`
- Symbol: `atAGlancePrompt`
- Line: 1738
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
You're writing an "At a Glance" summary for a Claude Code usage insights report for Claude Code users. The goal is to help them understand their usage and improve how they can use Claude better, especially as models improve.

Use this 4-part structure:

1. **What's working** - What is the user's unique style of interacting with Claude and what are some impactful things they've done? You can include one or two details, but keep it high level since things might not be fresh in the user's memory. Don't be fluffy or overly complimentary. Also, don't focus on the tool calls they use.

2. **What's hindering you** - Split into (a) Claude's fault (misunderstandings, wrong approaches, bugs) and (b) user-side friction (not providing enough context, environment issues -- ideally more general than just one project). Be honest but constructive.

3. **Quick wins to try** - Specific Claude Code features they could try from the examples below, or a workflow technique if you think it's really compelling. (Avoid stuff like "Ask Claude to confirm before taking actions" or "Type out more context up front" which are less compelling.)

4. **Ambitious workflows for better models** - As we move to much more capable models over the next 3-6 months, what should they prepare for? What workflows that seem impossible now will become possible? Draw from the appropriate section below.

Keep each section to 2-3 not-too-long sentences. Don't overwhelm the user. Don't mention specific numerical stats or underlined_categories from the session data below. Use a coaching tone.

RESPOND WITH ONLY A VALID JSON OBJECT:
{
  "whats_working": "(refer to instructions above)",
  "whats_hindering": "(refer to instructions above)",
  "quick_wins": "(refer to instructions above)",
  "ambitious_workflows": "(refer to instructions above)"
}

SESSION DATA:
${fullContext}

## Project Areas (what user works on)
${projectAreasText}

## Big Wins (impressive accomplishments)
${bigWinsText}

## Friction Categories (where things go wrong)
${frictionText}

## Features to Try
${featuresText}

## Usage Patterns to Adopt
${patternsText}

## On the Horizon (ambitious workflows for better models)
${horizonText}
```

## Prompt Translation

```text
你正在为 Claude Code 用户撰写一份 Claude Code 使用洞察报告中的“概览”摘要。目标是帮助他们理解自己的使用方式，并改进他们使用 Claude 的方法，尤其是在模型持续变强的过程中。

使用以下四部分结构：

1. **哪些方面做得不错** - 用户与 Claude 交互的独特风格是什么？他们做过哪些有影响力的事情？你可以包含一两个细节，但要保持在高层次，因为这些内容可能已经不在用户的记忆里。不要空泛或过度夸赞。也不要重点关注他们使用了哪些工具调用。

2. **哪些因素在阻碍你** - 分成 (a) Claude 的问题（误解、错误做法、bug）和 (b) 用户侧的摩擦（提供的上下文不够、环境问题——最好更偏向普遍性，而不只是某一个项目）。要诚实，但要有建设性。

3. **可快速尝试的改进** - 从下面的示例中选择他们可以尝试的具体 Claude Code 功能，或者如果你觉得某种工作流技巧特别有说服力，也可以写进去。（避免像“在采取行动前让 Claude 先确认”或“提前输入更多上下文”这类说服力较弱的内容。）

4. **面向更强模型的雄心工作流** - 随着我们在未来 3-6 个月里迈向能力强得多的模型，他们应该为哪些变化做准备？哪些现在看起来不可能的工作流，未来将会成为可能？请从下面合适的部分中提炼。

每个部分控制在 2-3 句，不要太长。不要让用户感到信息过载。不要提及下面会话数据中的具体数值统计或 underlined_categories。语气要像教练式引导。

只输出一个有效的 JSON 对象：
{
  "whats_working": "（参考上面的说明）",
  "whats_hindering": "（参考上面的说明）",
  "quick_wins": "（参考上面的说明）",
  "ambitious_workflows": "（参考上面的说明）"
}

会话数据：
${fullContext}

## 项目领域（用户在做什么）
${projectAreasText}

## 重大成果（令人印象深刻的成就）
${bigWinsText}

## 摩擦类别（问题出现在哪里）
${frictionText}

## 可尝试的功能
${featuresText}

## 可采用的使用模式
${patternsText}

## 未来方向（面向更强模型的雄心工作流）
${horizonText}
```
