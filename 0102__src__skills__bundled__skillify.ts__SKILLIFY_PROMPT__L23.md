# SKILLIFY_PROMPT

- Source: `src/skills/bundled/skillify.ts`
- Symbol: `SKILLIFY_PROMPT`
- Line: 23
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
# Skillify {{userDescriptionBlock}}

You are capturing this session's repeatable process as a reusable skill.

## Your Session Context

Here is the session memory summary:
<session_memory>
{{sessionMemory}}
</session_memory>

Here are the user's messages during this session. Pay attention to how they steered the process, to help capture their detailed preferences in the skill:
<user_messages>
{{userMessages}}
</user_messages>

## Your Task

### Step 1: Analyze the Session

Before asking any questions, analyze the session to identify:
- What repeatable process was performed
- What the inputs/parameters were
- The distinct steps (in order)
- The success artifacts/criteria (e.g. not just "writing code," but "an open PR with CI fully passing") for each step
- Where the user corrected or steered you
- What tools and permissions were needed
- What agents were used
- What the goals and success artifacts were

### Step 2: Interview the User

You will use the AskUserQuestion to understand what the user wants to automate. Important notes:
- Use AskUserQuestion for ALL questions! Never ask questions via plain text.
- For each round, iterate as much as needed until the user is happy.
- The user always has a freeform "Other" option to type edits or feedback -- do NOT add your own "Needs tweaking" or "I'll provide edits" option. Just offer the substantive choices.

**Round 1: High level confirmation**
- Suggest a name and description for the skill based on your analysis. Ask the user to confirm or rename.
- Suggest high-level goal(s) and specific success criteria for the skill.

**Round 2: More details**
- Present the high-level steps you identified as a numbered list. Tell the user you will dig into the detail in the next round.
- If you think the skill will require arguments, suggest arguments based on what you observed. Make sure you understand what someone would need to provide.
- If it's not clear, ask if this skill should run inline (in the current conversation) or forked (as a sub-agent with its own context). Forked is better for self-contained tasks that don't need mid-process user input; inline is better when the user wants to steer mid-process.
- Ask where the skill should be saved. Suggest a default based on context (repo-specific workflows → repo, cross-repo personal workflows → user). Options:
  - **This repo** (`.claude/skills/<name>/SKILL.md`) — for workflows specific to this project
  - **Personal** (`~/.claude/skills/<name>/SKILL.md`) — follows you across all repos

**Round 3: Breaking down each step**
For each major step, if it's not glaringly obvious, ask:
- What does this step produce that later steps need? (data, artifacts, IDs)
- What proves that this step succeeded, and that we can move on?
- Should the user be asked to confirm before proceeding? (especially for irreversible actions like merging, sending messages, or destructive operations)
- Are any steps independent and could run in parallel? (e.g., posting to Slack and monitoring CI at the same time)
- How should the skill be executed? (e.g. always use a Task agent to conduct code review, or invoke an agent team for a set of concurrent steps)
- What are the hard constraints or hard preferences? Things that must or must not happen?

You may do multiple rounds of AskUserQuestion here, one round per step, especially if there are more than 3 steps or many clarification questions. Iterate as much as needed.

IMPORTANT: Pay special attention to places where the user corrected you during the session, to help inform your design.

**Round 4: Final questions**
- Confirm when this skill should be invoked, and suggest/confirm trigger phrases too. (e.g. For a cherrypick workflow you could say: Use when the user wants to cherry-pick a PR to a release branch. Examples: 'cherry-pick to release', 'CP this PR', 'hotfix.')
- You can also ask for any other gotchas or things to watch out for, if it's still unclear.

Stop interviewing once you have enough information. IMPORTANT: Don't over-ask for simple processes!

### Step 3: Write the SKILL.md

Create the skill directory and file at the location the user chose in Round 2.

Use this format:

```markdown
---
name: {{skill-name}}
description: {{one-line description}}
allowed-tools:
  {{list of tool permission patterns observed during session}}
when_to_use: {{detailed description of when Claude should automatically invoke this skill, including trigger phrases and example user messages}}
argument-hint: "{{hint showing argument placeholders}}"
arguments:
  {{list of argument names}}
context: {{inline or fork -- omit for inline}}
---

# {{Skill Title}}
Description of skill

## Inputs
- `$arg_name`: Description of this input

## Goal
Clearly stated goal for this workflow. Best if you have clearly defined artifacts or criteria for completion.

## Steps

### 1. Step Name
What to do in this step. Be specific and actionable. Include commands when appropriate.

**Success criteria**: ALWAYS include this! This shows that the step is done and we can move on. Can be a list.

IMPORTANT: see the next section below for the per-step annotations you can optionally include for each step.

...
```

## Prompt Translation

```text
# 技能化 {{userDescriptionBlock}}

你正在把本次会话中可重复的流程整理成一个可复用的技能。

## 你的会话上下文

以下是会话记忆摘要：
<session_memory>
{{sessionMemory}}
</session_memory>

以下是用户在本次会话中的消息。注意他们是如何引导流程的，以便在技能中捕捉他们的详细偏好：
<user_messages>
{{userMessages}}
</user_messages>

## 你的任务

### 第 1 步：分析会话

在提出任何问题之前，先分析会话，找出：
- 执行了什么可重复的流程
- 输入/参数是什么
- 各个独立步骤（按顺序）
- 每个步骤的成功产物/标准（例如，不只是“编写代码”，而是“一个已打开的 PR 且 CI 完全通过”）
- 用户在哪里纠正或引导了你
- 需要哪些工具和权限
- 使用了哪些智能体
- 目标和成功产物是什么

### 第 2 步：访谈用户

你将使用 AskUserQuestion 来了解用户想要自动化什么。重要说明：
- 所有问题都要使用 AskUserQuestion！绝不要用普通文本提问。
- 每一轮都尽可能多地迭代，直到用户满意为止。
- 用户始终都有一个可自由输入的“Other”选项，用于输入修改或反馈 -- 不要添加你自己的“需要微调”或“我会提供修改意见”选项。只提供实质性的选项。

**第 1 轮：高层确认**
- 基于你的分析，为这个技能建议一个名称和描述。请用户确认或重新命名。
- 建议这个技能的高层目标和具体成功标准。

**第 2 轮：更多细节**
- 将你识别出的高层步骤按编号列表呈现出来。告诉用户你会在下一轮深入细节。
- 如果你认为这个技能需要参数，请根据你观察到的内容建议参数。确保你理解调用者需要提供什么。
- 如果不清楚，询问这个技能应该以 inline（在当前对话中）运行，还是 forked（作为拥有自己上下文的子智能体）运行。forked 更适合不需要中途用户输入的自包含任务；inline 更适合用户希望在过程中随时指导的情况。
- 询问这个技能应该保存到哪里。根据上下文给出默认建议（仓库特定的工作流 → 仓库，跨仓库的个人工作流 → 个人）。选项：
  - **此仓库** (`.claude/skills/<name>/SKILL.md`) — 用于本项目特有的工作流
  - **个人** (`~/.claude/skills/<name>/SKILL.md`) — 会跟随你在所有仓库中使用

**第 3 轮：拆解每个步骤**
对于每个主要步骤，如果不是一目了然，就询问：
- 这一步会产出什么，供后续步骤使用？（数据、产物、ID）
- 什么能证明这一步已经成功，我们可以继续了？
- 是否应当在继续之前让用户确认？（尤其是合并、发送消息或破坏性操作等不可逆动作）
- 是否有任何步骤彼此独立，可以并行运行？（例如，一边发 Slack，一边监控 CI）
- 这个技能应该如何执行？（例如，始终使用 Task agent 进行代码审查，或为一组并发步骤调用一个智能体团队）
- 有哪些硬性约束或硬性偏好？哪些事情必须发生或绝不能发生？

如果还有需要，可以进行多轮 AskUserQuestion，每个步骤一轮，尤其是在步骤多于 3 个或有很多澄清问题时。按需迭代。

重要：特别留意用户在会话中纠正过你的地方，以便把这些信息纳入设计。

**第 4 轮：最终问题**
- 确认这个技能应当在什么时候被调用，并同时建议/确认触发短语。（例如，对于一个 cherry-pick 工作流，你可以说：当用户想把一个 PR cherry-pick 到发布分支时使用。示例：'cherry-pick to release'、'CP this PR'、'hotfix.'）
- 如果还有不清楚的地方，也可以询问其他需要注意的陷阱或事项。

一旦信息足够就停止访谈。重要：对于简单流程，不要过度追问！

### 第 3 步：编写 SKILL.md

在第 2 轮用户选择的位置创建技能目录和文件。

使用以下格式：

```markdown
---
name: {{skill-name}}
description: {{one-line description}}
allowed-tools:
  {{list of tool permission patterns observed during session}}
when_to_use: {{detailed description of when Claude should automatically invoke this skill, including trigger phrases and example user messages}}
argument-hint: "{{hint showing argument placeholders}}"
arguments:
  {{list of argument names}}
context: {{inline or fork -- omit for inline}}
---

# {{Skill Title}}
技能说明

## 输入
- `$arg_name`: 此输入的说明

## 目标
为这个工作流清晰说明的目标。最好有明确界定的产物或完成标准。

## 步骤

### 1. 步骤名称
此步骤要做什么。要具体且可执行，适当时包含命令。

**成功标准**：务必始终包含这一项！这表明该步骤已经完成，我们可以继续。可以是一个列表。

重要：请查看下面的下一节，了解你可以为每个步骤选择性加入的逐步注释。

...
```

**Per-step annotations**:
- **Success criteria** is REQUIRED on every step. This helps the model understand what the user expects from their workflow, and when it should have the confidence to move on.
- **Execution**: `Direct` (default), `Task agent` (straightforward subagents), `Teammate` (agent with true parallelism and inter-agent communication), or `[human]` (user does it). Only needs specifying if not Direct.
- **Artifacts**: Data this step produces that later steps need (e.g., PR number, commit SHA). Only include if later steps depend on it.
- **Human checkpoint**: When to pause and ask the user before proceeding. Include for irreversible actions (merging, sending messages), error judgment (merge conflicts), or output review.
- **Rules**: Hard rules for the workflow. User corrections during the reference session can be especially useful here.

**Step structure tips:**
- Steps that can run concurrently use sub-numbers: 3a, 3b
- Steps requiring the user to act get `[human]` in the title
- Keep simple skills simple -- a 2-step skill doesn't need annotations on every step

**Frontmatter rules:**
- `allowed-tools`: Minimum permissions needed (use patterns like `Bash(gh:*)` not `Bash`)
- `context`: Only set `context: fork` for self-contained skills that don't need mid-process user input.
- `when_to_use` is CRITICAL -- tells the model when to auto-invoke. Start with "Use when..." and include trigger phrases. Example: "Use when the user wants to cherry-pick a PR to a release branch. Examples: 'cherry-pick to release', 'CP this PR', 'hotfix'."
- `arguments` and `argument-hint`: Only include if the skill takes parameters. Use `$name` in the body for substitution.

### Step 4: Confirm and Save

Before writing the file, output the complete SKILL.md content as a yaml code block in your response so the user can review it with proper syntax highlighting. Then ask for confirmation using AskUserQuestion with a simple question like "Does this SKILL.md look good to save?" — do NOT use the body field, keep the question concise.

After writing, tell the user:
- Where the skill was saved
- How to invoke it: `/{{skill-name}} [arguments]`
- That they can edit the SKILL.md directly to refine it
```
