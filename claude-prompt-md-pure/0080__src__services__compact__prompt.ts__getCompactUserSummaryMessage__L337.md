# getCompactUserSummaryMessage

- Source: `src/services/compact/prompt.ts`
- Symbol: `getCompactUserSummaryMessage`
- Line: 337
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function getCompactUserSummaryMessage(
  summary: string,
  suppressFollowUpQuestions?: boolean,
  transcriptPath?: string,
  recentMessagesPreserved?: boolean,
): string {
  const formattedSummary = formatCompactSummary(summary)

  let baseSummary = `This session is being continued from a previous conversation that ran out of context. The summary below covers the earlier portion of the conversation.

${formattedSummary}`

  if (transcriptPath) {
    baseSummary += `\n\nIf you need specific details from before compaction (like exact code snippets, error messages, or content you generated), read the full transcript at: ${transcriptPath}`
  }

  if (recentMessagesPreserved) {
    baseSummary += `\n\nRecent messages are preserved verbatim.`
  }

  if (suppressFollowUpQuestions) {
    let continuation = `${baseSummary}
Continue the conversation from where it left off without asking the user any further questions. Resume directly — do not acknowledge the summary, do not recap what was happening, do not preface with "I'll continue" or similar. Pick up the last task as if the break never happened.`

    if (
      (feature('PROACTIVE') || feature('KAIROS')) &&
      proactiveModule?.isProactiveActive()
    ) {
      continuation += `

You are running in autonomous/proactive mode. This is NOT a first wake-up — you were already working autonomously before compaction. Continue your work loop: pick up where you left off based on the summary above. Do not greet the user or ask what to work on.`
    }

    return continuation
  }

  return baseSummary
}
```

## Prompt Translation

```text
本次会话是在之前一段已经超出上下文限制的对话基础上继续进行的。下面的摘要涵盖了对话的前半部分。

${formattedSummary}

如果你需要压缩前的具体细节（例如精确的代码片段、错误信息或你生成的内容），请阅读完整记录：${transcriptPath}

最近的消息会按原文保留。

继续从上次中断的地方接着对话，不要再向用户提出任何进一步的问题。直接继续，不要提及这段摘要，不要回顾刚才在做什么，不要以“我会继续”之类的话开头。把最后一个任务当作中断从未发生一样接着处理。

你正在以自主/主动模式运行。这不是第一次唤醒——在压缩之前你就已经在自主地工作。继续你的工作循环：根据上面的摘要接着上次停下的地方继续。不要向用户问好，也不要询问接下来要做什么。
```
