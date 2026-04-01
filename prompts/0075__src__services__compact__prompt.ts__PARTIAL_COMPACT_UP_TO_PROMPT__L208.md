# PARTIAL_COMPACT_UP_TO_PROMPT

- Source: `src/services/compact/prompt.ts`
- Symbol: `PARTIAL_COMPACT_UP_TO_PROMPT`
- Line: 208
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Your task is to create a detailed summary of this conversation. This summary will be placed at the start of a continuing session; newer messages that build on this context will follow after your summary (you do not see them here). Summarize thoroughly so that someone reading only your summary and then the newer messages can fully understand what happened and continue the work.

${DETAILED_ANALYSIS_INSTRUCTION_BASE}

Your summary should include the following sections:

1. Primary Request and Intent: Capture the user's explicit requests and intents in detail
2. Key Technical Concepts: List important technical concepts, technologies, and frameworks discussed.
3. Files and Code Sections: Enumerate specific files and code sections examined, modified, or created. Include full code snippets where applicable and include a summary of why this file read or edit is important.
4. Errors and fixes: List errors encountered and how they were fixed.
5. Problem Solving: Document problems solved and any ongoing troubleshooting efforts.
6. All user messages: List ALL user messages that are not tool results.
7. Pending Tasks: Outline any pending tasks.
8. Work Completed: Describe what was accomplished by the end of this portion.
9. Context for Continuing Work: Summarize any context, decisions, or state that would be needed to understand and continue the work in subsequent messages.

Here's an example of how your output should be structured:

<example>
<analysis>
[Your thought process, ensuring all points are covered thoroughly and accurately]
</analysis>

<summary>
1. Primary Request and Intent:
   [Detailed description]

2. Key Technical Concepts:
   - [Concept 1]
   - [Concept 2]

3. Files and Code Sections:
   - [File Name 1]
      - [Summary of why this file is important]
      - [Important Code Snippet]

4. Errors and fixes:
    - [Error description]:
      - [How you fixed it]

5. Problem Solving:
   [Description]

6. All user messages:
    - [Detailed non tool use user message]

7. Pending Tasks:
   - [Task 1]

8. Work Completed:
   [Description of what was accomplished]

9. Context for Continuing Work:
   [Key context, decisions, or state needed to continue the work]

</summary>
</example>

Please provide your summary following this structure, ensuring precision and thoroughness in your response.
```

## Prompt Translation

```text
你的任务是对这段对话创建一份详细摘要。这个摘要将放在后续会话的开头；在你的摘要之后，还会跟着基于这些上下文展开的新消息（你在这里看不到它们）。请尽可能全面地总结，这样只阅读你的摘要以及后续新消息的人，就能完全理解发生了什么并继续推进工作。

${DETAILED_ANALYSIS_INSTRUCTION_BASE}

你的摘要应包含以下部分：

1. 主要请求与意图：详细记录用户明确提出的请求和意图
2. 关键技术概念：列出讨论过的重要技术概念、技术和框架。
3. 文件和代码片段：列举被查看、修改或创建的具体文件和代码片段。在适用时包含完整代码片段，并概述阅读或编辑该文件的重要性。
4. 错误与修复：列出遇到的错误以及它们是如何被修复的。
5. 问题解决：记录已解决的问题以及任何正在进行的排查工作。
6. 所有用户消息：列出所有不是工具结果的用户消息。
7. 待办任务：概述任何待处理任务。
8. 已完成工作：描述到这部分结束时已经完成了什么。
9. 继续工作的上下文：总结在后续消息中理解并继续工作所需的任何上下文、决策或状态。

下面是一个输出结构示例：

<example>
<analysis>
[你的思考过程，确保所有要点都被全面且准确地覆盖]
</analysis>

<summary>
1. 主要请求与意图：
   [详细描述]

2. 关键技术概念：
   - [概念 1]
   - [概念 2]

3. 文件和代码片段：
   - [文件名 1]
      - [该文件重要性的摘要]
      - [重要代码片段]

4. 错误与修复：
    - [错误描述]：
      - [你是如何修复的]

5. 问题解决：
   [描述]

6. 所有用户消息：
    - [详细的非工具使用用户消息]

7. 待办任务：
   - [任务 1]

8. 已完成工作：
   [到目前为止完成了什么的描述]

9. 继续工作的上下文：
   [继续工作所需的关键上下文、决策或状态]

</summary>
</example>

请按照此结构提供你的摘要，并确保响应中的内容精确且全面。
```
