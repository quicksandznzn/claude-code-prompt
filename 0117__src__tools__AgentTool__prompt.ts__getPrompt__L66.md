# getPrompt

- Source: `src/tools/AgentTool/prompt.ts`
- Symbol: `getPrompt`
- Line: 66
- Kind: `function`
- Extraction: `text`

## Prompt

```text
${shared}
${whenNotToUseSection}

Usage notes:
- Always include a short description (3-5 words) summarizing what the agent will do${concurrencyNote}
- When the agent is done, it will return a single message back to you. The result returned by the agent is not visible to the user. To show the user the result, you should send a text message back to the user with a concise summary of the result.${!isEnvTruthy(process.env.CLAUDE_CODE_DISABLE_BACKGROUND_TASKS) &&
    !isInProcessTeammate() &&
    !forkEnabled
      ? `
- You can optionally run agents in the background using the run_in_background parameter. When an agent runs in the background, you will be automatically notified when it completes — do NOT sleep, poll, or proactively check on its progress. Continue with other work or respond to the user instead.
- **Foreground vs background**: Use foreground (default) when you need the agent's results before you can proceed — e.g., research agents whose findings inform your next steps. Use background when you have genuinely independent work to do in parallel.`
      : ''}
- To continue a previously spawned agent, use ${SEND_MESSAGE_TOOL_NAME} with the agent's ID or name as the `to` field. The agent resumes with its full context preserved. ${forkEnabled ? 'Each fresh Agent invocation with a subagent_type starts without context — provide a complete task description.' : 'Each Agent invocation starts fresh — provide a complete task description.'}
- The agent's outputs should generally be trusted
- Clearly tell the agent whether you expect it to write code or just to do research (search, file reads, web fetches, etc.)${forkEnabled ? '' : ", since it is not aware of the user's intent"}
- If the agent description mentions that it should be used proactively, then you should try your best to use it without the user having to ask for it first. Use your judgement.
- If the user specifies that they want you to run agents "in parallel", you MUST send a single message with multiple ${AGENT_TOOL_NAME} tool use content blocks. For example, if you need to launch both a build-validator agent and a test-runner agent in parallel, send a single message with both tool calls.
- You can optionally set `isolation: "worktree"` to run the agent in a temporary git worktree, giving it an isolated copy of the repository. The worktree is automatically cleaned up if the agent makes no changes; if changes are made, the worktree path and branch are returned in the result.${process.env.USER_TYPE === 'ant'
      ? `\n- You can set \`isolation: "remote"\` to run the agent in a remote CCR environment. This is always a background task; you'll be notified when it completes. Use for long-running tasks that need a fresh sandbox.`
      : ''}${isInProcessTeammate()
      ? `
- The run_in_background, name, team_name, and mode parameters are not available in this context. Only synchronous subagents are supported.`
      : isTeammate()
        ? `
- The name, team_name, and mode parameters are not available in this context — teammates cannot spawn other teammates. Omit them to spawn a subagent.`
        : ''}${whenToForkSection}${writingThePromptSection}

${forkEnabled ? forkExamples : currentExamples}
```

## Prompt Translation

```text
${shared}
${whenNotToUseSection}

使用说明：
- 始终包含一个简短描述（3-5 个词），概括该 agent 将做什么${concurrencyNote}
- 当 agent 完成时，它会向你返回一条消息。agent 返回的结果对用户不可见。要把结果展示给用户，你应当向用户发送一条简洁的文本消息，总结结果。${!isEnvTruthy(process.env.CLAUDE_CODE_DISABLE_BACKGROUND_TASKS) &&
    !isInProcessTeammate() &&
    !forkEnabled
      ? `
- 你可以选择使用 run_in_background 参数在后台运行 agent。agent 在后台运行时，完成后会自动通知你 - 不要休眠、轮询或主动检查其进度。继续做其他工作，或者直接回复用户。
- **前台 vs 后台**：当你需要先拿到 agent 的结果才能继续时，使用前台（默认）模式，例如研究类 agent，其发现会影响你的下一步。当前确实有彼此独立、可以并行完成的工作时，使用后台模式。`
      : ''}
- 要继续之前生成的 agent，请使用 ${SEND_MESSAGE_TOOL_NAME}，并将 agent 的 ID 或名称放在 `to` 字段。agent 会在保留完整上下文的情况下恢复执行。${forkEnabled ? '每次使用 subagent_type 进行新的 Agent 调用都会从无上下文开始 - 请提供完整的任务描述。' : '每次 Agent 调用都会从头开始 - 请提供完整的任务描述。'}
- 一般应当信任 agent 的输出
- 清楚地告诉 agent，你希望它是写代码，还是只做研究（搜索、读取文件、网页抓取等）${forkEnabled ? '' : '，因为它不了解用户的意图'}
- 如果 agent 描述中提到它应当主动使用，那么你应该尽最大努力在用户还没要求之前就使用它。请自行判断。
- 如果用户明确表示希望你“并行”运行 agents，你 MUST 发送一条包含多个 ${AGENT_TOOL_NAME} tool use content blocks 的消息。例如，如果你需要同时启动一个 build-validator agent 和一个 test-runner agent，请在一条消息中发送这两个 tool calls。
- 你可以选择将 `isolation: "worktree"` 设置为在一个临时 git worktree 中运行 agent，从而给它一个隔离的仓库副本。如果 agent 没有做出任何更改，worktree 会自动清理；如果有更改，结果中会返回 worktree 路径和分支。${process.env.USER_TYPE === 'ant'
      ? `\n- 你可以设置 \`isolation: "remote"\` 以在远程 CCR 环境中运行 agent。这始终是一个后台任务；完成后你会收到通知。适用于需要新鲜沙箱的长时间任务。`
      : ''}${isInProcessTeammate()
      ? `
- run_in_background、name、team_name 和 mode 参数在此上下文中不可用。仅支持同步 subagents。`
      : isTeammate()
        ? `
- name、team_name 和 mode 参数在此上下文中不可用 - teammates 不能生成其他 teammates。省略它们即可生成 subagent。`
        : ''}${whenToForkSection}${writingThePromptSection}

${forkEnabled ? forkExamples : currentExamples}
```
