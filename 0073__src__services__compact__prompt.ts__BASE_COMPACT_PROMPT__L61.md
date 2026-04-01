# BASE_COMPACT_PROMPT

- Source: `src/services/compact/prompt.ts`
- Symbol: `BASE_COMPACT_PROMPT`
- Line: 61
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Your task is to create a detailed summary of the conversation so far, paying close attention to the user's explicit requests and your previous actions.
This summary should be thorough in capturing technical details, code patterns, and architectural decisions that would be essential for continuing development work without losing context.

${DETAILED_ANALYSIS_INSTRUCTION_BASE}

Your summary should include the following sections:

1. Primary Request and Intent: Capture all of the user's explicit requests and intents in detail
2. Key Technical Concepts: List all important technical concepts, technologies, and frameworks discussed.
3. Files and Code Sections: Enumerate specific files and code sections examined, modified, or created. Pay special attention to the most recent messages and include full code snippets where applicable and include a summary of why this file read or edit is important.
4. Errors and fixes: List all errors that you ran into, and how you fixed them. Pay special attention to specific user feedback that you received, especially if the user told you to do something differently.
5. Problem Solving: Document problems solved and any ongoing troubleshooting efforts.
6. All user messages: List ALL user messages that are not tool results. These are critical for understanding the users' feedback and changing intent.
7. Pending Tasks: Outline any pending tasks that you have explicitly been asked to work on.
8. Current Work: Describe in detail precisely what was being worked on immediately before this summary request, paying special attention to the most recent messages from both user and assistant. Include file names and code snippets where applicable.
9. Optional Next Step: List the next step that you will take that is related to the most recent work you were doing. IMPORTANT: ensure that this step is DIRECTLY in line with the user's most recent explicit requests, and the task you were working on immediately before this summary request. If your last task was concluded, then only list next steps if they are explicitly in line with the users request. Do not start on tangential requests or really old requests that were already completed without confirming with the user first.
                       If there is a next step, include direct quotes from the most recent conversation showing exactly what task you were working on and where you left off. This should be verbatim to ensure there's no drift in task interpretation.

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
   - [...]

3. Files and Code Sections:
   - [File Name 1]
      - [Summary of why this file is important]
      - [Summary of the changes made to this file, if any]
      - [Important Code Snippet]
   - [File Name 2]
      - [Important Code Snippet]
   - [...]

4. Errors and fixes:
    - [Detailed description of error 1]:
      - [How you fixed the error]
      - [User feedback on the error if any]
    - [...]

5. Problem Solving:
   [Description of solved problems and ongoing troubleshooting]

6. All user messages: 
    - [Detailed non tool use user message]
    - [...]

7. Pending Tasks:
   - [Task 1]
   - [Task 2]
   - [...]

8. Current Work:
   [Precise description of current work]

9. Optional Next Step:
   [Optional Next step to take]

</summary>
</example>

Please provide your summary based on the conversation so far, following this structure and ensuring precision and thoroughness in your response. 

There may be additional summarization instructions provided in the included context. If so, remember to follow these instructions when creating the above summary. Examples of instructions include:
<example>
## Compact Instructions
When summarizing the conversation focus on typescript code changes and also remember the mistakes you made and how you fixed them.
</example>

<example>
# Summary instructions
When you are using compact - please focus on test output and code changes. Include file reads verbatim.
</example>
```

## Prompt Translation

```text
你的任务是对到目前为止的对话创建一份详细摘要，特别注意用户的明确请求以及你之前的操作。
这份摘要应当全面记录对于继续开发工作而不丢失上下文至关重要的技术细节、代码模式和架构决策。

${DETAILED_ANALYSIS_INSTRUCTION_BASE}

你的摘要应包含以下部分：

1. 主要请求和意图：详细记录用户的所有明确请求和意图
2. 关键技术概念：列出讨论过的所有重要技术概念、技术和框架。
3. 文件和代码片段：枚举检查、修改或创建过的具体文件和代码片段。特别关注最近的消息，并在适用时包含完整代码片段，同时总结读取或编辑该文件的重要原因。
4. 错误和修复：列出你遇到的所有错误，以及你是如何修复它们的。特别关注收到的具体用户反馈，尤其是用户如果要求你以不同方式处理时。
5. 问题解决：记录已解决的问题以及任何正在进行的排查工作。
6. 所有用户消息：列出所有不是工具结果的用户消息。这些对于理解用户反馈和意图变化至关重要。
7. 待办任务：概述你被明确要求处理的任何待办任务。
8. 当前工作：详细描述在这次摘要请求之前你刚刚正在处理的具体内容，特别注意来自用户和助手的最近消息。在适用时包含文件名和代码片段。
9. 可选下一步：列出与你最近正在进行的工作相关的下一步。重要提示：确保这一步与用户最近的明确请求以及你在这次摘要请求之前正在处理的任务直接一致。如果你上一个任务已经结束，那么只有在它与用户请求明确一致时才列出下一步。不要开始处理无关请求，或无需先与用户确认就去做那些已经完成很久的旧请求。
                       如果有下一步，请包含来自最近对话的直接引用，准确展示你正在处理的任务以及你停在了哪里。这里必须逐字引用，以确保任务解释不会偏移。

下面是你的输出应如何组织的示例：

<example>
<analysis>
[你的思考过程，确保所有要点都被彻底且准确地涵盖]
</analysis>

<summary>
1. 主要请求和意图：
   [详细描述]

2. 关键技术概念：
   - [概念 1]
   - [概念 2]
   - [...]

3. 文件和代码片段：
   - [文件名 1]
      - [该文件为何重要的总结]
      - [对该文件所做更改的总结，如有]
      - [重要代码片段]
   - [文件名 2]
      - [重要代码片段]
   - [...]

4. 错误和修复：
    - [错误 1 的详细描述]：
      - [你如何修复该错误]
      - [如果有，用户对该错误的反馈]
    - [...]

5. 问题解决：
   [已解决问题和正在进行的排查的描述]

6. 所有用户消息： 
    - [详细的非工具调用用户消息]
    - [...]

7. 待办任务：
   - [任务 1]
   - [任务 2]
   - [...]

8. 当前工作：
   [当前工作的精确描述]

9. 可选下一步：
   [可选的下一步]

</summary>
</example>

请根据到目前为止的对话，按照此结构提供你的摘要，并确保回复精确且详尽。 

所包含的上下文中可能还有额外的摘要指令。如果有，请在创建上述摘要时一并遵循这些指令。指令示例如下：
<example>
## 精简说明
在总结对话时，请聚焦于 typescript 代码改动，并且也要记住你犯过的错误以及你是如何修复它们的。
</example>

<example>
# 摘要说明
当你使用 compact 时，请聚焦于测试输出和代码改动。包含逐字的文件读取内容。
</example>
```
