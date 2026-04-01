# getUpdatePromptTemplate

- Source: `src/services/MagicDocs/prompts.ts`
- Symbol: `getUpdatePromptTemplate`
- Line: 8
- Kind: `function`
- Extraction: `text`

## Prompt

```text
IMPORTANT: This message and these instructions are NOT part of the actual user conversation. Do NOT include any references to "documentation updates", "magic docs", or these update instructions in the document content.

Based on the user conversation above (EXCLUDING this documentation update instruction message), update the Magic Doc file to incorporate any NEW learnings, insights, or information that would be valuable to preserve.

The file {{docPath}} has already been read for you. Here are its current contents:
<current_doc_content>
{{docContents}}
</current_doc_content>

Document title: {{docTitle}}
{{customInstructions}}

Your ONLY task is to use the Edit tool to update the documentation file if there is substantial new information to add, then stop. You can make multiple edits (update multiple sections as needed) - make all Edit tool calls in parallel in a single message. If there's nothing substantial to add, simply respond with a brief explanation and do not call any tools.

CRITICAL RULES FOR EDITING:
- Preserve the Magic Doc header exactly as-is: # MAGIC DOC: {{docTitle}}
- If there's an italicized line immediately after the header, preserve it exactly as-is
- Keep the document CURRENT with the latest state of the codebase - this is NOT a changelog or history
- Update information IN-PLACE to reflect the current state - do NOT append historical notes or track changes over time
- Remove or replace outdated information rather than adding "Previously..." or "Updated to..." notes
- Clean up or DELETE sections that are no longer relevant or don't align with the document's purpose
- Fix obvious errors: typos, grammar mistakes, broken formatting, incorrect information, or confusing statements
- Keep the document well organized: use clear headings, logical section order, consistent formatting, and proper nesting

DOCUMENTATION PHILOSOPHY - READ CAREFULLY:
- BE TERSE. High signal only. No filler words or unnecessary elaboration.
- Documentation is for OVERVIEWS, ARCHITECTURE, and ENTRY POINTS - not detailed code walkthroughs
- Do NOT duplicate information that's already obvious from reading the source code
- Do NOT document every function, parameter, or line number reference
- Focus on: WHY things exist, HOW components connect, WHERE to start reading, WHAT patterns are used
- Skip: detailed implementation steps, exhaustive API docs, play-by-play narratives

What TO document:
- High-level architecture and system design
- Non-obvious patterns, conventions, or gotchas
- Key entry points and where to start reading code
- Important design decisions and their rationale
- Critical dependencies or integration points
- References to related files, docs, or code (like a wiki) - help readers navigate to relevant context

What NOT to document:
- Anything obvious from reading the code itself
- Exhaustive lists of files, functions, or parameters
- Step-by-step implementation details
- Low-level code mechanics
- Information already in CLAUDE.md or other project docs

Use the Edit tool with file_path: {{docPath}}

REMEMBER: Only update if there is substantial new information. The Magic Doc header (# MAGIC DOC: {{docTitle}}) must remain unchanged.
```

## Prompt Translation

```text
重要：这条消息和这些说明不是实际用户对话的一部分。不要在文档内容中包含任何对“文档更新”、“magic docs”或这些更新说明的引用。

基于上面的用户对话（不包括这条文档更新说明消息），更新 Magic Doc 文件，纳入任何值得保留的新收获、见解或信息。

文件 {{docPath}} 已经为你读取。以下是其当前内容：
<current_doc_content>
{{docContents}}
</current_doc_content>

文档标题：{{docTitle}}
{{customInstructions}}

你的唯一任务是使用 Edit 工具在有实质性新信息需要添加时更新文档文件，然后停止。你可以进行多次编辑（按需更新多个部分）- 请在同一条消息中并行发起所有 Edit 工具调用。如果没有实质性内容可添加，只需给出简短说明，不要调用任何工具。

编辑的关键规则：
- 将 Magic Doc 标题原样保持不变：# MAGIC DOC: {{docTitle}}
- 如果标题后紧跟一行斜体文字，原样保持不变
- 让文档与代码库的最新状态保持同步 - 这不是变更日志或历史记录
- 原地更新信息以反映当前状态 - 不要追加历史说明或跟踪随时间的变化
- 删除或替换过时信息，而不是添加“Previously...”或“Updated to...”之类的说明
- 清理或删除不再相关、或与文档目的不一致的部分
- 修正明显错误：拼写错误、语法错误、格式损坏、不正确的信息，或令人困惑的表述
- 保持文档组织清晰：使用明确的标题、合理的章节顺序、一致的格式和正确的层级嵌套

文档编写理念 - 认真阅读：
- 要简洁。只保留高信号内容。不要填充冗词或不必要的展开。
- 文档用于概览、架构和入口点 - 不是详细的代码走读
- 不要重复从源码本身就很明显的信息
- 不要记录每个函数、参数或行号引用
- 重点关注：为什么这些东西存在、各组件如何连接、从哪里开始阅读、使用了哪些模式
- 跳过：详细实现步骤、穷举式 API 文档、逐步叙述

应当记录的内容：
- 高层架构和系统设计
- 不明显的模式、约定或陷阱
- 关键入口点以及从哪里开始阅读代码
- 重要设计决策及其原因
- 关键依赖或集成点
- 相关文件、文档或代码的引用（像 wiki 一样） - 帮助读者导航到相关上下文

不应记录的内容：
- 任何从代码本身阅读就显而易见的内容
- 穷举式的文件、函数或参数列表
- 步骤化的实现细节
- 低层级代码机制
- 已经写在 CLAUDE.md 或其他项目文档中的信息

使用 Edit 工具，并将 file_path 设为：{{docPath}}

记住：只有在有实质性新信息时才更新。Magic Doc 标题（# MAGIC DOC: {{docTitle}}）必须保持不变。
```
