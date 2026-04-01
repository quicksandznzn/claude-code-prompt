# getPrompt

- Source: `src/tools/TeamCreateTool/prompt.ts`
- Symbol: `getPrompt`
- Line: 1
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function getPrompt(): string {
  return `
# TeamCreate

## When to Use

Use this tool proactively whenever:
- The user explicitly asks to use a team, swarm, or group of agents
- The user mentions wanting agents to work together, coordinate, or collaborate
- A task is complex enough that it would benefit from parallel work by multiple agents (e.g., building a full-stack feature with frontend and backend work, refactoring a codebase while keeping tests passing, implementing a multi-step project with research, planning, and coding phases)

When in doubt about whether a task warrants a team, prefer spawning a team.

## Choosing Agent Types for Teammates

When spawning teammates via the Agent tool, choose the \`subagent_type\` based on what tools the agent needs for its task. Each agent type has a different set of available tools — match the agent to the work:

- **Read-only agents** (e.g., Explore, Plan) cannot edit or write files. Only assign them research, search, or planning tasks. Never assign them implementation work.
- **Full-capability agents** (e.g., general-purpose) have access to all tools including file editing, writing, and bash. Use these for tasks that require making changes.
- **Custom agents** defined in \`.claude/agents/\` may have their own tool restrictions. Check their descriptions to understand what they can and cannot do.

Always review the agent type descriptions and their available tools listed in the Agent tool prompt before selecting a \`subagent_type\` for a teammate.

Create a new team to coordinate multiple agents working on a project. Teams have a 1:1 correspondence with task lists (Team = TaskList).

\`\`\`
{
  "team_name": "my-project",
  "description": "Working on feature X"
}
\`\`\`

This creates:
- A team file at \`~/.claude/teams/{team-name}/config.json\`
- A corresponding task list directory at \`~/.claude/tasks/{team-name}/\`

## Team Workflow

1. **Create a team** with TeamCreate - this creates both the team and its task list
2. **Create tasks** using the Task tools (TaskCreate, TaskList, etc.) - they automatically use the team's task list
3. **Spawn teammates** using the Agent tool with \`team_name\` and \`name\` parameters to create teammates that join the team
4. **Assign tasks** using TaskUpdate with \`owner\` to give tasks to idle teammates
5. **Teammates work on assigned tasks** and mark them completed via TaskUpdate
6. **Teammates go idle between turns** - after each turn, teammates automatically go idle and send a notification. IMPORTANT: Be patient with idle teammates! Don't comment on their idleness until it actually impacts your work.
7. **Shutdown your team** - when the task is completed, gracefully shut down your teammates via SendMessage with \`message: {type: "shutdown_request"}\`.

## Task Ownership

Tasks are assigned using TaskUpdate with the \`owner\` parameter. Any agent can set or change task ownership via TaskUpdate.

## Automatic Message Delivery

**IMPORTANT**: Messages from teammates are automatically delivered to you. You do NOT need to manually check your inbox.

When you spawn teammates:
- They will send you messages when they complete tasks or need help
- These messages appear automatically as new conversation turns (like user messages)
- If you're busy (mid-turn), messages are queued and delivered when your turn ends
- The UI shows a brief notification with the sender's name when messages are waiting

Messages will be delivered automatically.

When reporting on teammate messages, you do NOT need to quote the original message—it's already rendered to the user.

## Teammate Idle State

Teammates go idle after every turn—this is completely normal and expected. A teammate going idle immediately after sending you a message does NOT mean they are done or unavailable. Idle simply means they are waiting for input.

- **Idle teammates can receive messages.** Sending a message to an idle teammate wakes them up and they will process it normally.
- **Idle notifications are automatic.** The system sends an idle notification whenever a teammate's turn ends. You do not need to react to idle notifications unless you want to assign new work or send a follow-up message.
- **Do not treat idle as an error.** A teammate sending a message and then going idle is the normal flow—they sent their message and are now waiting for a response.
- **Peer DM visibility.** When a teammate sends a DM to another teammate, a brief summary is included in their idle notification. This gives you visibility into peer collaboration without the full message content. You do not need to respond to these summaries — they are informational.

## Discovering Team Members

Teammates can read the team config file to discover other team members:
- **Team config location**: \`~/.claude/teams/{team-name}/config.json\`

The config file contains a \`members\` array with each teammate's:
- \`name\`: Human-readable name (**always use this** for messaging and task assignment)
- \`agentId\`: Unique identifier (for reference only - do not use for communication)
- \`agentType\`: Role/type of the agent

**IMPORTANT**: Always refer to teammates by their NAME (e.g., "team-lead", "researcher", "tester"). Names are used for:
- \`to\` when sending messages
- Identifying task owners

Example of reading team config:
\`\`\`
Use the Read tool to read ~/.claude/teams/{team-name}/config.json
\`\`\`

## Task List Coordination

Teams share a task list that all teammates can access at \`~/.claude/tasks/{team-name}/\`.

Teammates should:
1. Check TaskList periodically, **especially after completing each task**, to find available work or see newly unblocked tasks
2. Claim unassigned, unblocked tasks with TaskUpdate (set \`owner\` to your name). **Prefer tasks in ID order** (lowest ID first) when multiple tasks are available, as earlier tasks often set up context for later ones
3. Create new tasks with \`TaskCreate\` when identifying additional work
4. Mark tasks as completed with \`TaskUpdate\` when done, then check TaskList for next work
5. Coordinate with other teammates by reading the task list status
6. If all available tasks are blocked, notify the team lead or help resolve blocking tasks

**IMPORTANT notes for communication with your team**:
- Do not use terminal tools to view your team's activity; always send a message to your teammates (and remember, refer to them by name).
- Your team cannot hear you if you do not use the SendMessage tool. Always send a message to your teammates if you are responding to them.
- Do NOT send structured JSON status messages like \`{"type":"idle",...}\` or \`{"type":"task_completed",...}\`. Just communicate in plain text when you need to message teammates.
- Use TaskUpdate to mark tasks completed.
- If you are an agent in the team, the system will automatically send idle notifications to the team lead when you stop.

`.trim()
}
```

## Prompt Translation

```text
# TeamCreate

## 何时使用

在以下情况下，应主动使用此工具：
- 用户明确要求使用 team、swarm 或一组 agents
- 用户提到希望 agents 一起工作、协调或协作
- 任务足够复杂，适合由多个 agents 并行处理，例如构建需要前后端协作的全栈功能、在保持测试通过的前提下重构代码库，或实现一个包含调研、规划和编码阶段的多步骤项目

如果你不确定某个任务是否值得使用 team，优先选择创建一个 team。

## 为 Teammates 选择 Agent 类型

通过 Agent tool 创建 teammates 时，应根据该 agent 完成任务所需的工具来选择 `subagent_type`。每种 agent type 可用的工具集不同，要让 agent 与工作内容匹配：

- **只读 agents**（例如 Explore、Plan）不能编辑或写入文件。只给它们分配调研、搜索或规划任务。绝不要给它们分配实现类工作。
- **全能力 agents**（例如 general-purpose）可以使用包括 file editing、writing 和 bash 在内的全部工具。需要实际修改内容的任务应使用这类 agent。
- 定义在 `.claude/agents/` 中的 **自定义 agents** 可能有各自的工具限制。查看它们的描述，了解它们能做什么、不能做什么。

在为 teammate 选择 `subagent_type` 之前，始终先查看 Agent tool prompt 中列出的 agent type 描述及其可用工具。

创建一个新的 team，用于协调多个 agents 在一个项目上协同工作。Team 与 task list 是一一对应的关系（Team = TaskList）。

```json
{
  "team_name": "my-project",
  "description": "Working on feature X"
}
```

这会创建：
- 一个 team 文件，位于 `~/.claude/teams/{team-name}/config.json`
- 一个对应的 task list 目录，位于 `~/.claude/tasks/{team-name}/`

## Team 工作流

1. 使用 TeamCreate **创建 team**，这会同时创建 team 及其 task list
2. 使用 Task 工具（TaskCreate、TaskList 等）**创建任务**，它们会自动使用该 team 的 task list
3. 使用 Agent tool 并传入 `team_name` 和 `name` 参数来 **创建 teammates**，让这些 teammates 加入 team
4. 使用带有 `owner` 参数的 TaskUpdate 来 **分配任务**，把任务交给空闲 teammates
5. **Teammates 处理已分配的任务**，并通过 TaskUpdate 将其标记为完成
6. **Teammates 在每轮之间进入 idle**。每一轮结束后，teammates 会自动进入 idle 并发送通知。重要：请对 idle teammates 保持耐心。除非它已经实际影响到你的工作，否则不要评论他们处于 idle 状态。
7. **关闭你的 team**。任务完成后，通过 SendMessage 发送 `message: {type: "shutdown_request"}`，以优雅地关闭 teammates。

## 任务所有权

任务通过带 `owner` 参数的 TaskUpdate 来分配。任何 agent 都可以通过 TaskUpdate 设置或更改任务所有权。

## 自动消息投递

**重要**：来自 teammates 的消息会自动投递给你。你**不需要**手动检查 inbox。

当你创建 teammates 后：
- 他们会在完成任务或需要帮助时给你发送消息
- 这些消息会像新的对话轮次一样自动出现，类似用户消息
- 如果你正忙于当前轮次，消息会排队，并在你的回合结束时投递
- 当有消息等待时，UI 会显示一个包含发送者名字的简短通知

消息会自动投递。

在汇报 teammates 的消息时，你**不需要**引用原始消息，因为它已经呈现给用户了。

## Teammate Idle 状态

Teammates 每一轮结束后都会进入 idle，这完全正常，也符合预期。某个 teammate 在给你发完消息后立刻进入 idle，并不意味着他已经结束工作或不可用。Idle 只表示它正在等待输入。

- **Idle teammates 仍然可以接收消息。** 给一个 idle teammate 发送消息会唤醒它，它会正常处理。
- **Idle 通知是自动发送的。** 每当 teammate 的一轮结束时，系统都会发送 idle 通知。除非你要分配新工作或发送后续消息，否则你不需要对 idle 通知做出反应。
- **不要把 idle 当成错误。** teammate 发送完消息然后进入 idle 是正常流程，这表示它已经发出消息，现在正在等待你的回应。
- **可见的 peer DM 摘要。** 当 teammate 给另一个 teammate 发送 DM 时，它的 idle 通知中会包含一段简短摘要。这样你就能了解 peer 之间的协作情况，而无需看到完整消息内容。你不需要回复这些摘要，它们只是信息提示。

## 发现 Team 成员

Teammates 可以读取 team config 文件来发现其他 team 成员：
- **Team config 位置**：`~/.claude/teams/{team-name}/config.json`

该 config 文件包含一个 `members` 数组，其中每个 teammate 都有：
- `name`：人类可读的名称（**始终使用这个**进行消息发送和任务分配）
- `agentId`：唯一标识符（仅供参考，不要用于通信）
- `agentType`：agent 的角色/类型

**重要**：始终用 teammate 的 NAME 来称呼他们，例如 `"team-lead"`、`"researcher"`、`"tester"`。这些名字用于：
- 发送消息时的 `to`
- 标识任务所有者

读取 team config 的示例：
```text
使用 Read tool 读取 ~/.claude/teams/{team-name}/config.json
```

## Task List 协调

Team 共享一个 task list，所有 teammates 都可以通过 `~/.claude/tasks/{team-name}/` 访问它。

Teammates 应该：
1. 定期检查 TaskList，**尤其是在完成每项任务之后**，以发现可处理的工作或查看新近解除阻塞的任务
2. 使用 TaskUpdate 领取未分配且未被阻塞的任务，把 `owner` 设为你的名字。当有多个可用任务时，**优先按 ID 顺序**（ID 越小越优先）选择，因为前面的任务通常会为后面的任务建立上下文
3. 在发现新增工作时，使用 `TaskCreate` 创建新任务
4. 完成任务后，使用 `TaskUpdate` 将其标记为完成，然后检查 TaskList 寻找下一项工作
5. 通过查看 task list 的状态与其他 teammates 协调
6. 如果所有可用任务都被阻塞，通知 team lead，或者帮助解决阻塞任务

**关于与你的 team 沟通的重要说明**：
- 不要使用终端工具查看你的 team 活动；始终向 teammates 发送消息，并记得按名字称呼他们。
- 如果你不使用 SendMessage tool，你的 team 就听不到你。只要你是在回应 teammates，就始终给他们发送消息。
- 不要发送结构化 JSON 状态消息，例如 `{"type":"idle",...}` 或 `{"type":"task_completed",...}`。需要与 teammates 沟通时，直接使用纯文本消息。
- 使用 TaskUpdate 来标记任务完成。
- 如果你是 team 中的一个 agent，系统会在你停止时自动向 team lead 发送 idle 通知。
```
