# PROMPT

- Source: `src/tools/TaskGetTool/prompt.ts`
- Symbol: `PROMPT`
- Line: 3
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Use this tool to retrieve a task by its ID from the task list.

## When to Use This Tool

- When you need the full description and context before starting work on a task
- To understand task dependencies (what it blocks, what blocks it)
- After being assigned a task, to get complete requirements

## Output

Returns full task details:
- **subject**: Task title
- **description**: Detailed requirements and context
- **status**: 'pending', 'in_progress', or 'completed'
- **blocks**: Tasks waiting on this one to complete
- **blockedBy**: Tasks that must complete before this one can start

## Tips

- After fetching a task, verify its blockedBy list is empty before beginning work.
- Use TaskList to see all tasks in summary form.
```

## Prompt Translation

```text
使用此工具根据任务 ID 从任务列表中检索任务。

## 何时使用此工具

- 当你在开始处理任务之前需要完整的描述和上下文时
- 当你需要了解任务依赖关系（它阻塞什么、又被什么阻塞）时
- 在被分配任务之后，用于获取完整需求

## 输出

返回完整任务详情：
- **subject**: 任务标题
- **description**: 详细需求和上下文
- **status**: 'pending'、'in_progress' 或 'completed'
- **blocks**: 正在等待该任务完成的任务
- **blockedBy**: 必须先完成、该任务才能开始的任务

## 提示

- 获取任务后，在开始工作之前先确认其 blockedBy 列表为空。
- 使用 TaskList 以摘要形式查看所有任务。
```
