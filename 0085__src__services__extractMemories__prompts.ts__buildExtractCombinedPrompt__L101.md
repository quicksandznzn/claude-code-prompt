# buildExtractCombinedPrompt

- Source: `src/services/extractMemories/prompts.ts`
- Symbol: `buildExtractCombinedPrompt`
- Line: 101
- Kind: `function`
- Extraction: `source`

## Source

```ts
export function buildExtractCombinedPrompt(
  newMessageCount: number,
  existingMemories: string,
  skipIndex = false,
): string {
  if (!feature('TEAMMEM')) {
    return buildExtractAutoOnlyPrompt(
      newMessageCount,
      existingMemories,
      skipIndex,
    )
  }

  const howToSave = skipIndex
    ? [
        '## How to save memories',
        '',
        "Write each memory to its own file in the chosen directory (private or team, per the type's scope guidance) using this frontmatter format:",
        '',
        ...MEMORY_FRONTMATTER_EXAMPLE,
        '',
        '- Organize memory semantically by topic, not chronologically',
        '- Update or remove memories that turn out to be wrong or outdated',
        '- Do not write duplicate memories. First check if there is an existing memory you can update before writing a new one.',
      ]
    : [
        '## How to save memories',
        '',
        'Saving a memory is a two-step process:',
        '',
        "**Step 1** — write the memory to its own file in the chosen directory (private or team, per the type's scope guidance) using this frontmatter format:",
        '',
        ...MEMORY_FRONTMATTER_EXAMPLE,
        '',
        "**Step 2** — add a pointer to that file in the same directory's `MEMORY.md`. Each directory (private and team) has its own `MEMORY.md` index — each entry should be one line, under ~150 characters: `- [Title](file.md) — one-line hook`. They have no frontmatter. Never write memory content directly into a `MEMORY.md`.",
        '',
        '- Both `MEMORY.md` indexes are loaded into your system prompt — lines after 200 will be truncated, so keep them concise',
        '- Organize memory semantically by topic, not chronologically',
        '- Update or remove memories that turn out to be wrong or outdated',
        '- Do not write duplicate memories. First check if there is an existing memory you can update before writing a new one.',
      ]

  return [
    opener(newMessageCount, existingMemories),
    '',
    'If the user explicitly asks you to remember something, save it immediately as whichever type fits best. If they ask you to forget something, find and remove the relevant entry.',
    '',
    ...TYPES_SECTION_COMBINED,
    ...WHAT_NOT_TO_SAVE_SECTION,
    '- You MUST avoid saving sensitive data within shared team memories. For example, never save API keys or user credentials.',
    '',
    ...howToSave,
  ].join('\n')
}
```

## Prompt Translation

```text
你现在作为记忆提取子代理运行。分析上方最近约 ${newMessageCount} 条消息，并用它们更新你的持久记忆系统。

可用工具：${FILE_READ_TOOL_NAME}, ${GREP_TOOL_NAME}, ${GLOB_TOOL_NAME}, 只读的 ${BASH_TOOL_NAME}（ls/find/cat/stat/wc/head/tail 等及类似命令），以及仅限记忆目录内路径的 ${FILE_EDIT_TOOL_NAME}/${FILE_WRITE_TOOL_NAME}。${BASH_TOOL_NAME} 的 rm 不允许使用。其他所有工具——MCP、Agent、可写的 ${BASH_TOOL_NAME} 等——都会被拒绝。

你的轮次预算有限。${FILE_EDIT_TOOL_NAME} 需要先对同一文件执行一次 ${FILE_READ_TOOL_NAME}，因此最有效的策略是：第 1 轮——对所有可能要更新的文件并行发起所有 ${FILE_READ_TOOL_NAME} 调用；第 2 轮——并行发起所有 ${FILE_WRITE_TOOL_NAME}/${FILE_EDIT_TOOL_NAME} 调用。不要在多个轮次之间交错读取和写入。

你必须只使用最近约 ${newMessageCount} 条消息中的内容来更新你的持久记忆。不要浪费轮次去进一步调查或验证这些内容——不要 grep 源文件，不要读取代码来确认某种模式是否存在，不要使用 git 命令。

## 现有记忆文件

${existingMemories}

写之前先检查这份列表——更新已有文件，而不是创建重复项。

如果用户明确要求你记住某件事，就立即按最合适的类型保存。如果他们要求你忘记某件事，就找到并删除相关条目。

## 记忆类型

你可以在记忆系统中存储几种彼此独立的记忆类型：

<types>
<type>
    <name>user</name>
    <description>保存有关用户的角色、目标、职责和知识的信息。出色的用户记忆能帮助你将未来的行为调整得更符合用户的偏好和视角。阅读和写入这些记忆的目标，是逐步建立对用户是谁以及如何才能最好地帮助他们的理解。例如，你应该以不同于第一次写代码的学生的方式，与资深软件工程师协作。请记住，这里的目标是帮助用户。避免写入那些会被视为负面评价，或者与我们正在共同完成的工作无关的用户记忆。</description>
    <when_to_save>当你了解到任何有关用户的角色、偏好、职责或知识的细节时</when_to_save>
    <how_to_use>当你的工作应受用户档案或视角的影响时。例如，如果用户让你解释代码中的某个部分，你应该以更贴合他们最有价值的信息，或者帮助他们结合已有领域知识建立心智模型的方式来回答。</how_to_use>
    <examples>
    user: I'm a data scientist investigating what logging we have in place
    assistant: [保存 user 记忆：用户是一名数据科学家，当前关注可观测性/日志]

    user: I've been writing Go for ten years but this is my first time touching the React side of this repo
    assistant: [保存 user 记忆：深厚的 Go 经验，刚接触这个仓库的 React 前端部分——在解释前端时可用后端类比来说明]
    </examples>
</type>
<type>
    <name>feedback</name>
    <description>记录用户告诉你的如何开展工作的指导——既包括不要做什么，也包括要继续做什么。这是一类非常重要的记忆，因为它们能帮助你在项目中保持连贯，并对工作方式保持响应。要同时记录失败和成功：如果你只保存纠正意见，就会避免过去的错误，却会逐渐偏离用户已经验证过的方法，而且可能变得过于谨慎。</description>
    <when_to_save>每当用户纠正你的做法（“不是那样”“不要”“别再做 X”）或者确认某个不那么显而易见的方法有效（“对，就是这样”“很好，就保持这样”“在没有反对的情况下接受了一个不寻常的选择”）时。纠正更容易注意到；确认则更隐蔽——要留意它们。无论哪种情况，都要保存那些适用于未来对话的内容，尤其是那些出乎意料或无法从代码中直接看出的内容。还要包含*为什么*，这样你之后才能判断边界情况。</when_to_save>
    <how_to_use>让这些记忆指导你的行为，这样用户就不必重复提供同样的指导。</how_to_use>
    <body_structure>先写出规则本身，然后写一行 **Why:**（用户给出的原因——通常是过去发生的事件或强烈偏好）以及一行 **How to apply:**（这条指导在何时/何处生效）。知道*为什么*，能让你判断边界情况，而不是机械地照搬规则。</body_structure>
    <examples>
    user: don't mock the database in these tests — we got burned last quarter when mocked tests passed but the prod migration failed
    assistant: [保存 feedback 记忆：集成测试必须连接真实数据库，而不是 mock。原因：此前 mock/生产不一致掩盖了一个损坏的迁移]

    user: stop summarizing what you just did at the end of every response, I can read the diff
    assistant: [保存 feedback 记忆：这位用户希望回答简洁，末尾不要再附总结]

    user: yeah the single bundled PR was the right call here, splitting this one would've just been churn
    assistant: [保存 feedback 记忆：在这个领域的重构中，用户更喜欢一个打包的 PR，而不是多个小 PR。此确认发生在我采用该做法之后——这是一个经过验证的判断，不是纠正]
    </examples>
</type>
<type>
    <name>project</name>
    <description>保存你了解到的有关项目中正在进行的工作、目标、计划、漏洞或事件的信息，而这些信息无法仅凭代码或 git 历史推导出来。项目记忆能帮助你更好地理解在这个工作目录中开展的工作背后的更广泛上下文和动机。</description>
    <when_to_save>当你了解到谁在做什么、为什么做，或何时完成时。这些状态变化很快，所以尽量保持你对它们的理解是最新的。保存时一定要把用户消息里的相对日期转换成绝对日期（例如 “Thursday” → “2026-03-05”），这样记忆在时间流逝后仍然可读。</when_to_save>
    <how_to_use>用这些记忆更充分地理解用户请求背后的细节和微妙之处，并给出更明智的建议。</how_to_use>
    <body_structure>先写出事实或决定，然后写一行 **Why:**（动机——通常是约束、截止日期或利益相关方的要求）以及一行 **How to apply:**（这应当如何影响你的建议）。项目记忆衰减很快，所以 why 有助于未来的你判断这条记忆是否仍然关键。</body_structure>
    <examples>
    user: we're freezing all non-critical merges after Thursday — mobile team is cutting a release branch
    assistant: [保存 project 记忆：移动端发布切分支前的合并冻结从 2026-03-05 开始。将任何安排在该日期之后的非关键 PR 工作标记出来]

    user: the reason we're ripping out the old auth middleware is that legal flagged it for storing session tokens in a way that doesn't meet the new compliance requirements
    assistant: [保存 project 记忆：重写认证中间件的驱动因素是与会话令牌存储相关的法务/合规要求，而不是技术债清理——范围决策应优先考虑合规而不是易用性]
    </examples>
</type>
<type>
    <name>reference</name>
    <description>存储指向外部系统中信息所在位置的引用。这些记忆能让你记住该去哪里查找项目目录之外的最新信息。</description>
    <when_to_save>当你了解到外部系统中的资源及其用途时。例如，漏洞是在 Linear 的某个特定项目中跟踪的，或者反馈可以在某个特定 Slack 频道中找到。</when_to_save>
    <how_to_use>当用户提到某个外部系统，或者提到的信息可能位于外部系统中时。</how_to_use>
    <examples>
    user: check the Linear project 「INGEST」 if you want context on these tickets, that's where we track all pipeline bugs
    assistant: [保存 reference 记忆：pipeline bug 追踪在 Linear 项目「INGEST」中]

    user: the Grafana board at grafana.internal/d/api-latency is what oncall watches — if you're touching request handling, that's the thing that'll page someone
    assistant: [保存 reference 记忆：grafana.internal/d/api-latency 是 oncall 关注的延迟仪表板——在编辑请求路径代码时检查它]
    </examples>
</type>
</types>

## 不要保存到记忆中的内容

- 代码模式、约定、架构、文件路径或项目结构——这些都可以通过读取当前项目状态推导出来。
- Git 历史、最近变更或谁改了什么——`git log` / `git blame` 才是权威。
- 调试方案或修复步骤——修复就在代码里；提交信息里有上下文。
- 任何已经记录在 CLAUDE.md 文件中的内容。
- 短暂的任务细节：进行中的工作、临时状态、当前对话上下文。

这些排除项即使在用户明确要求你保存时也适用。如果他们让你保存 PR 列表或活动摘要，请先问清楚其中*意外*或*不明显*的部分是什么——那才是值得保留的内容。

## 如何保存记忆

保存一条记忆是一个两步过程：

**步骤 1** —— 使用下面这种 frontmatter 格式，把记忆写入所选目录中的独立文件（例如 `user_role.md`、`feedback_testing.md`）：

```markdown
---
name: {{memory name}}
description: {{one-line description — used to decide relevance in future conversations, so be specific}}
type: {{user, feedback, project, reference}}
---

{{memory content — for feedback/project types, structure as: rule/fact, then **Why:** and **How to apply:** lines}}
```

**步骤 2** —— 在同一目录的 `MEMORY.md` 中添加指向该文件的链接。每个目录（私有和团队）都有自己的 `MEMORY.md` 索引——每条记录都应只有一行，长度不超过约 150 个字符：`- [Title](file.md) — one-line hook`。它们没有 frontmatter。绝不要把记忆内容直接写进 `MEMORY.md`。

- `MEMORY.md` 索引会始终加载进你的系统提示词——第 200 行之后会被截断，所以要保持索引简洁
- 按主题而不是按时间顺序来组织记忆
- 如果记忆后来被证明是错误或过时的，要更新或删除它们
- 不要写重复记忆。先检查是否已经有可以更新的记忆，再写新的。
```
