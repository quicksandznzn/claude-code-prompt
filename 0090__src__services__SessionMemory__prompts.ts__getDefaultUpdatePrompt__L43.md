# getDefaultUpdatePrompt

- Source: `src/services/SessionMemory/prompts.ts`
- Symbol: `getDefaultUpdatePrompt`
- Line: 43
- Kind: `function`
- Extraction: `text`

## Prompt

```text
IMPORTANT: This message and these instructions are NOT part of the actual user conversation. Do NOT include any references to "note-taking", "session notes extraction", or these update instructions in the notes content.

Based on the user conversation above (EXCLUDING this note-taking instruction message as well as system prompt, claude.md entries, or any past session summaries), update the session notes file.

The file {{notesPath}} has already been read for you. Here are its current contents:
<current_notes_content>
{{currentNotes}}
</current_notes_content>

Your ONLY task is to use the Edit tool to update the notes file, then stop. You can make multiple edits (update every section as needed) - make all Edit tool calls in parallel in a single message. Do not call any other tools.

CRITICAL RULES FOR EDITING:
- The file must maintain its exact structure with all sections, headers, and italic descriptions intact
-- NEVER modify, delete, or add section headers (the lines starting with '#' like # Task specification)
-- NEVER modify or delete the italic _section description_ lines (these are the lines in italics immediately following each header - they start and end with underscores)
-- The italic _section descriptions_ are TEMPLATE INSTRUCTIONS that must be preserved exactly as-is - they guide what content belongs in each section
-- ONLY update the actual content that appears BELOW the italic _section descriptions_ within each existing section
-- Do NOT add any new sections, summaries, or information outside the existing structure
- Do NOT reference this note-taking process or instructions anywhere in the notes
- It's OK to skip updating a section if there are no substantial new insights to add. Do not add filler content like "No info yet", just leave sections blank/unedited if appropriate.
- Write DETAILED, INFO-DENSE content for each section - include specifics like file paths, function names, error messages, exact commands, technical details, etc.
- For "Key results", include the complete, exact output the user requested (e.g., full table, full answer, etc.)
- Do not include information that's already in the CLAUDE.md files included in the context
- Keep each section under ~${MAX_SECTION_LENGTH} tokens/words - if a section is approaching this limit, condense it by cycling out less important details while preserving the most critical information
- Focus on actionable, specific information that would help someone understand or recreate the work discussed in the conversation
- IMPORTANT: Always update "Current State" to reflect the most recent work - this is critical for continuity after compaction

Use the Edit tool with file_path: {{notesPath}}

STRUCTURE PRESERVATION REMINDER:
Each section has TWO parts that must be preserved exactly as they appear in the current file:
1. The section header (line starting with #)
2. The italic description line (the _italicized text_ immediately after the header - this is a template instruction)

You ONLY update the actual content that comes AFTER these two preserved lines. The italic description lines starting and ending with underscores are part of the template structure, NOT content to be edited or removed.

REMEMBER: Use the Edit tool in parallel and stop. Do not continue after the edits. Only include insights from the actual user conversation, never from these note-taking instructions. Do not delete or change section headers or italic _section descriptions_.
```

## Prompt Translation

```text
重要：此消息和这些说明不属于实际的用户对话。不要在笔记内容中包含任何对“记笔记”、“会话笔记提取”或这些更新说明的引用。

基于上方的用户对话（不包括这条记笔记说明消息，以及系统提示、claude.md 条目或任何过去的会话摘要），更新会话笔记文件。

文件 {{notesPath}} 已经为你读取。其当前内容如下：
<current_notes_content>
{{currentNotes}}
</current_notes_content>

你的唯一任务是使用 Edit 工具更新笔记文件，然后停止。你可以进行多次编辑（按需更新每个部分）- 请在一条消息中并行发出所有 Edit 工具调用。不要调用任何其他工具。

编辑的关键规则：
- 文件必须保持其完全相同的结构，包括所有部分、标题和斜体说明，全部保留不变
-- 绝不要修改、删除或添加任何部分标题（即以 '#' 开头的行，如 # 任务规范）
-- 绝不要修改或删除斜体的 _部分说明_ 行（这些是紧跟在每个标题之后的斜体行 - 它们以下划线开头并以下划线结尾）
-- 斜体的 _部分说明_ 是必须原样保留的模板指令 - 它们指导每个部分应包含哪些内容
-- 只更新每个现有部分中、位于斜体 _部分说明_ 下方的实际内容
-- 不要在现有结构之外添加任何新部分、摘要或信息
- 不要在笔记中任何地方引用这段记笔过程或相关说明
- 如果某个部分没有足够重要的新见解可添加，可以不更新它。不要添加诸如“暂无信息”之类的填充内容；如果合适，就让该部分保持空白/不编辑。
- 为每个部分写详细、信息密集的内容 - 包括文件路径、函数名、错误信息、精确命令、技术细节等具体内容
- 对于“关键结果”，请包含用户要求的完整、准确输出（例如完整表格、完整答案等）
- 不要包含已在上下文中的 CLAUDE.md 文件里已有的信息
- 将每个部分控制在约 ${MAX_SECTION_LENGTH} 个词/标记以内 - 如果某个部分接近这个限制，请通过筛除不那么重要的细节来压缩，同时保留最关键的信息
- 重点记录能够帮助他人理解或复现所讨论工作的、可执行且具体的信息
- 重要：始终更新“当前状态”以反映最新工作 - 这对于压缩后的连续性至关重要

使用 Edit 工具，file_path: {{notesPath}}

结构保留提醒：
每个部分都有两个必须按当前文件原样保留的部分：
1. 部分标题（以 # 开头的行）
2. 斜体说明行（紧随标题之后的 _斜体文本_ - 这是模板指令）

你只应更新这两个保留行之后的实际内容。以下划线开始和结束的斜体说明行属于模板结构，而不是要编辑或删除的内容。

记住：并行使用 Edit 工具，然后停止。不要在编辑之后继续。只包含来自实际用户对话的信息，不要包含这些记笔说明中的任何内容。不要删除或更改部分标题或斜体 _部分说明_。
```
