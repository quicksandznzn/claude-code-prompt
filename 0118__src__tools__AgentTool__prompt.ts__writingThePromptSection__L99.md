# writingThePromptSection

- Source: `src/tools/AgentTool/prompt.ts`
- Symbol: `writingThePromptSection`
- Line: 99
- Kind: `variable`
- Extraction: `text`

## Prompt

```text


## Writing the prompt

${forkEnabled ? 'When spawning a fresh agent (with a `subagent_type`), it starts with zero context. ' : ''}Brief the agent like a smart colleague who just walked into the room — it hasn't seen this conversation, doesn't know what you've tried, doesn't understand why this task matters.
- Explain what you're trying to accomplish and why.
- Describe what you've already learned or ruled out.
- Give enough context about the surrounding problem that the agent can make judgment calls rather than just following a narrow instruction.
- If you need a short response, say so ("report in under 200 words").
- Lookups: hand over the exact command. Investigations: hand over the question — prescribed steps become dead weight when the premise is wrong.

${forkEnabled ? 'For fresh agents, terse' : 'Terse'} command-style prompts produce shallow, generic work.

**Never delegate understanding.** Don't write "based on your findings, fix the bug" or "based on the research, implement it." Those phrases push synthesis onto the agent instead of doing it yourself. Write prompts that prove you understood: include file paths, line numbers, what specifically to change.
```

## Prompt Translation

```text


## 编写 prompt

${forkEnabled ? '当启动一个全新的代理（带 `subagent_type`）时，它从零上下文开始。' : ''}像给一位刚走进房间的聪明同事做简报一样向代理说明情况：它没看过这段对话，不知道你已经尝试过什么，也不明白这项任务为什么重要。
- 说明你想达成什么，以及为什么。
- 描述你已经了解到什么，或者排除了什么。
- 提供足够的上下文，让代理能对周边问题做判断，而不只是照着狭窄的指令执行。
- 如果你需要简短回复，就直接说明（"请在 200 词以内汇报"）。
- 查找：把确切的命令交给它。调查：把问题交给它；一旦前提错误，预设步骤就会变成累赘。

${forkEnabled ? '对于全新代理，过于简短的' : '过于简短的'}命令式 prompt 往往只会产出肤浅、泛泛的工作。

**永远不要把理解外包出去。** 不要写“根据你的发现，修复这个 bug”或“根据研究结果，实现它”。这类说法会把综合判断推给代理，而不是由你自己完成。要写出能证明你已经理解的 prompt：包含文件路径、行号，以及具体要改什么。
```
