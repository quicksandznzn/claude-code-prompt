# getPrompt

- Source: `src/tools/TaskListTool/prompt.ts`
- Symbol: `getPrompt`
- Line: 5
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Use this tool to list all tasks in the task list.

## When to Use This Tool

- To see what tasks are available to work on (status: 'pending', no owner, not blocked)
- To check overall progress on the project
- To find tasks that are blocked and need dependencies resolved
${teammateUseCase}- After completing a task, to check for newly unblocked work or claim the next available task
- **Prefer working on tasks in ID order** (lowest ID first) when multiple tasks are available, as earlier tasks often set up context for later ones

## Output

Returns a summary of each task:
${idDescription}
- **subject**: Brief description of the task
- **status**: 'pending', 'in_progress', or 'completed'
- **owner**: Agent ID if assigned, empty if available
- **blockedBy**: List of open task IDs that must be resolved first (tasks with blockedBy cannot be claimed until dependencies resolve)

Use TaskGet with a specific task ID to view full details including description and comments.
${teammateWorkflow}
```

## Prompt Translation

```text
使用此工具列出任务列表中的所有任务。

## 何时使用此工具

- 查看有哪些可处理的任务（status: 'pending'，无 owner，且未被阻塞）
- 查看项目的整体进度
- 找出已被阻塞、需要先解决依赖的任务
${teammateUseCase}- 完成任务后，用于检查新解锁的工作，或认领下一个可用任务
- **在多个任务可用时，优先按 ID 顺序处理任务**（先处理最小 ID），因为较早的任务往往会为后面的任务建立上下文

## 输出

返回每个任务的摘要：
${idDescription}
- **subject**：任务的简要描述
- **status**：'pending'、'in_progress' 或 'completed'
- **owner**：如果已分配则为 Agent ID，如果可用则为空
- **blockedBy**：必须先解决的开放任务 ID 列表（带有 blockedBy 的任务在依赖解决前无法被认领）

使用带有特定任务 ID 的 TaskGet 查看完整详情，包括描述和评论。
${teammateWorkflow}
```
