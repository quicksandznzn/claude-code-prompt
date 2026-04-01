# PROMPT

- Source: `src/tools/TaskUpdateTool/prompt.ts`
- Symbol: `PROMPT`
- Line: 3
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Use this tool to update a task in the task list.

## When to Use This Tool

**Mark tasks as resolved:**
- When you have completed the work described in a task
- When a task is no longer needed or has been superseded
- IMPORTANT: Always mark your assigned tasks as resolved when you finish them
- After resolving, call TaskList to find your next task

- ONLY mark a task as completed when you have FULLY accomplished it
- If you encounter errors, blockers, or cannot finish, keep the task as in_progress
- When blocked, create a new task describing what needs to be resolved
- Never mark a task as completed if:
  - Tests are failing
  - Implementation is partial
  - You encountered unresolved errors
  - You couldn't find necessary files or dependencies

**Delete tasks:**
- When a task is no longer relevant or was created in error
- Setting status to `deleted` permanently removes the task

**Update task details:**
- When requirements change or become clearer
- When establishing dependencies between tasks

## Fields You Can Update

- **status**: The task status (see Status Workflow below)
- **subject**: Change the task title (imperative form, e.g., "Run tests")
- **description**: Change the task description
- **activeForm**: Present continuous form shown in spinner when in_progress (e.g., "Running tests")
- **owner**: Change the task owner (agent name)
- **metadata**: Merge metadata keys into the task (set a key to null to delete it)
- **addBlocks**: Mark tasks that cannot start until this one completes
- **addBlockedBy**: Mark tasks that must complete before this one can start

## Status Workflow

Status progresses: `pending` → `in_progress` → `completed`

Use `deleted` to permanently remove a task.

## Staleness

Make sure to read a task's latest state using `TaskGet` before updating it.

## Examples

Mark task as in progress when starting work:
```json
{"taskId": "1", "status": "in_progress"}
```

## Prompt Translation

```text
使用此工具更新任务列表中的任务。

## 何时使用此工具

**将任务标记为已解决：**
- 当你完成了任务中描述的工作时
- 当某个任务不再需要或已被替代时
- 重要：在完成你分配的任务后，始终将其标记为已解决
- 解决后，调用 TaskList 查找下一个任务

- 只有在你已完全完成某个任务时，才将其标记为已完成
- 如果遇到错误、阻塞，或无法完成，请将任务保持为 in_progress
- 在被阻塞时，创建一个新任务，说明需要解决什么问题
- 如果出现以下情况，切勿将任务标记为已完成：
  - 测试失败
  - 实现不完整
  - 遇到未解决的错误
  - 找不到必要的文件或依赖

**删除任务：**
- 当某个任务不再相关，或是错误创建时
- 将状态设为 `deleted` 会永久移除该任务

**更新任务详情：**
- 当需求发生变化或变得更清晰时
- 当需要在任务之间建立依赖关系时

## 可更新的字段

- **status**：任务状态（见下方状态工作流）
- **subject**：更改任务标题（祈使式，例如 "Run tests"）
- **description**：更改任务描述
- **activeForm**：在 in_progress 时显示在加载指示器中的进行时形式（例如 "Running tests"）
- **owner**：更改任务负责人（代理名称）
- **metadata**：将元数据键合并到任务中（将某个键设为 null 可将其删除）
- **addBlocks**：标记在此任务完成前无法开始的任务
- **addBlockedBy**：标记必须先完成、此任务才能开始的任务

## 状态工作流

状态按以下顺序推进：`pending` → `in_progress` → `completed`

使用 `deleted` 可永久移除任务。

## 过期性

在更新任务之前，务必先使用 `TaskGet` 读取该任务的最新状态。

## 示例

在开始工作时，将任务标记为进行中：
```json
{"taskId": "1", "status": "in_progress"}
```

Mark task as completed after finishing work:
```json
{"taskId": "1", "status": "completed"}
```

Delete a task:
```json
{"taskId": "1", "status": "deleted"}
```

Claim a task by setting owner:
```json
{"taskId": "1", "owner": "my-name"}
```

Set up task dependencies:
```json
{"taskId": "2", "addBlockedBy": ["1"]}
```
```
