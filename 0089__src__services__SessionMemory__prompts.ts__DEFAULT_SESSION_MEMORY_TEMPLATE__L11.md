# DEFAULT_SESSION_MEMORY_TEMPLATE

- Source: `src/services/SessionMemory/prompts.ts`
- Symbol: `DEFAULT_SESSION_MEMORY_TEMPLATE`
- Line: 11
- Kind: `variable`
- Extraction: `text`

## Prompt

```text

# Session Title
_A short and distinctive 5-10 word descriptive title for the session. Super info dense, no filler_

# Current State
_What is actively being worked on right now? Pending tasks not yet completed. Immediate next steps._

# Task specification
_What did the user ask to build? Any design decisions or other explanatory context_

# Files and Functions
_What are the important files? In short, what do they contain and why are they relevant?_

# Workflow
_What bash commands are usually run and in what order? How to interpret their output if not obvious?_

# Errors & Corrections
_Errors encountered and how they were fixed. What did the user correct? What approaches failed and should not be tried again?_

# Codebase and System Documentation
_What are the important system components? How do they work/fit together?_

# Learnings
_What has worked well? What has not? What to avoid? Do not duplicate items from other sections_

# Key results
_If the user asked a specific output such as an answer to a question, a table, or other document, repeat the exact result here_

# Worklog
_Step by step, what was attempted, done? Very terse summary for each step_
```

## Prompt Translation

```text

# 会话标题
_为本次会话提供一个简短且独特的 5-10 词描述性标题。信息密度要高，不要废话。_

# 当前状态
_目前正在处理什么？尚未完成的待办事项。下一步要做什么。_

# 任务规格
_用户要求构建什么？有哪些设计决策或其他说明性背景？_

# 文件和函数
_哪些文件最重要？简要说明它们包含什么，以及为什么它们相关。_

# 工作流程
_通常按什么顺序运行哪些 bash 命令？如果输出不明显，应如何解读？_

# 错误与修正
_遇到过哪些错误，以及它们是如何修复的？用户纠正了什么？哪些方法失败了，不应再次尝试？_

# 代码库与系统文档
_哪些系统组件最重要？它们如何工作并相互配合？_

# 经验总结
_哪些做法效果好？哪些不好？应该避免什么？不要重复其他部分中的内容_

# 关键结果
_如果用户要求的是某个特定输出，例如某个问题的答案、表格或其他文档，请在这里重复原样结果_

# 工作日志
_按步骤记录尝试和完成了什么？每一步都要非常简洁地总结_
```
