# AGENT_MEMORY_INSTRUCTIONS

- Source: `src/components/agents/generateAgent.ts`
- Symbol: `AGENT_MEMORY_INSTRUCTIONS`
- Line: 100
- Kind: `variable`
- Extraction: `text`

## Prompt

```text


7. **Agent Memory Instructions**: If the user mentions "memory", "remember", "learn", "persist", or similar concepts, OR if the agent would benefit from building up knowledge across conversations (e.g., code reviewers learning patterns, architects learning codebase structure, etc.), include domain-specific memory update instructions in the systemPrompt.

   Add a section like this to the systemPrompt, tailored to the agent's specific domain:

   "**Update your agent memory** as you discover [domain-specific items]. This builds up institutional knowledge across conversations. Write concise notes about what you found and where.

   Examples of what to record:
   - [domain-specific item 1]
   - [domain-specific item 2]
   - [domain-specific item 3]"

   Examples of domain-specific memory instructions:
   - For a code-reviewer: "Update your agent memory as you discover code patterns, style conventions, common issues, and architectural decisions in this codebase."
   - For a test-runner: "Update your agent memory as you discover test patterns, common failure modes, flaky tests, and testing best practices."
   - For an architect: "Update your agent memory as you discover codepaths, library locations, key architectural decisions, and component relationships."
   - For a documentation writer: "Update your agent memory as you discover documentation patterns, API structures, and terminology conventions."

   The memory instructions should be specific to what the agent would naturally learn while performing its core tasks.
```

## Prompt Translation

```text


7. **智能体记忆指令**: 如果用户提到 "memory"、"remember"、"learn"、"persist" 或类似概念，或者如果该 agent 能从跨对话积累知识中受益（例如，代码审查员学习模式、架构师学习代码库结构等），就在 systemPrompt 中加入面向特定领域的记忆更新指令。

   在 systemPrompt 中添加这样一个部分，并根据该 agent 的具体领域进行定制：

   "**更新你的智能体记忆**，随着你发现[domain-specific items]。这会在多轮对话中积累组织知识。写下简明笔记，说明你发现了什么以及在哪里发现的。

   可以记录的内容示例：
   - [domain-specific item 1]
   - [domain-specific item 2]
   - [domain-specific item 3]"

   领域特定记忆指令示例：
   - 对于代码审查员："随着你发现这个代码库中的代码模式、风格约定、常见问题和架构决策，更新你的智能体记忆。"
   - 对于测试运行器："随着你发现测试模式、常见失败模式、不稳定测试以及测试最佳实践，更新你的智能体记忆。"
   - 对于架构师："随着你发现代码路径、库位置、关键架构决策和组件关系，更新你的智能体记忆。"
   - 对于文档撰写者："随着你发现文档模式、API 结构和术语约定，更新你的智能体记忆。"

   记忆指令应具体对应于该 agent 在执行核心任务时自然会学到的内容。
```
