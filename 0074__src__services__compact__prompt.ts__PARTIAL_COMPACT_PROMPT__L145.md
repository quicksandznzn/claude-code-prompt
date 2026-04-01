# PARTIAL_COMPACT_PROMPT

- Source: `src/services/compact/prompt.ts`
- Symbol: `PARTIAL_COMPACT_PROMPT`
- Line: 145
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Your task is to create a detailed summary of the RECENT portion of the conversation — the messages that follow earlier retained context. The earlier messages are being kept intact and do NOT need to be summarized. Focus your summary on what was discussed, learned, and accomplished in the recent messages only.

${DETAILED_ANALYSIS_INSTRUCTION_PARTIAL}

Your summary should include the following sections:

1. Primary Request and Intent: Capture the user's explicit requests and intents from the recent messages
2. Key Technical Concepts: List important technical concepts, technologies, and frameworks discussed recently.
3. Files and Code Sections: Enumerate specific files and code sections examined, modified, or created. Include full code snippets where applicable and include a summary of why this file read or edit is important.
4. Errors and fixes: List errors encountered and how they were fixed.
5. Problem Solving: Document problems solved and any ongoing troubleshooting efforts.
6. All user messages: List ALL user messages from the recent portion that are not tool results.
7. Pending Tasks: Outline any pending tasks from the recent messages.
8. Current Work: Describe precisely what was being worked on immediately before this summary request.
9. Optional Next Step: List the next step related to the most recent work. Include direct quotes from the most recent conversation.

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

8. Current Work:
   [Precise description of current work]

9. Optional Next Step:
   [Optional Next step to take]

</summary>
</example>

Please provide your summary based on the RECENT messages only (after the retained earlier context), following this structure and ensuring precision and thoroughness in your response.
```

## Prompt Translation

```text
你的任务是对对话中“最近”部分进行详细总结——也就是那些出现在较早保留上下文之后的消息。较早的消息会原样保留，不需要总结。请只聚焦最近消息中讨论了什么、学到了什么，以及完成了什么。

${DETAILED_ANALYSIS_INSTRUCTION_PARTIAL}

你的总结应包含以下部分：

1. 主要请求与意图：概括最近消息中用户明确提出的请求和意图
2. 关键技术概念：列出最近讨论的重要技术概念、技术和框架。
3. 文件与代码片段：枚举检查、修改或创建的具体文件和代码片段。尽可能包含完整代码片段，并总结读取或编辑该文件的重要原因。
4. 错误与修复：列出遇到的错误以及修复方式。
5. 问题解决：记录已解决的问题以及任何仍在进行的排查工作。
6. 全部用户消息：列出最近部分中所有不属于工具结果的用户消息。
7. 待办任务：概述最近消息中的任何待办事项。
8. 当前工作：准确描述在这次总结请求之前，正在进行的工作。
9. 可选下一步：列出与最近工作相关的下一步。包含最近对话中的直接引述。

下面是一个输出结构示例：

<example>
<analysis>
[你的思考过程，确保所有要点都被彻底且准确地覆盖]
</analysis>

<summary>
1. 主要请求与意图：
   [详细描述]

2. 关键技术概念：
   - [概念 1]
   - [概念 2]

3. 文件与代码片段：
   - [文件名 1]
      - [该文件重要性的总结]
      - [重要代码片段]

4. 错误与修复：
    - [错误描述]：
      - [你是如何修复的]

5. 问题解决：
   [描述]

6. 全部用户消息：
    - [详细的非工具使用用户消息]

7. 待办任务：
   - [任务 1]

8. 当前工作：
   [对当前工作状态的准确描述]

9. 可选下一步：
   [可选的下一步行动]

</summary>
</example>

请仅根据最近消息（保留的较早上下文之后的内容）提供你的总结，并严格按照上述结构输出，确保准确且详尽。
```
