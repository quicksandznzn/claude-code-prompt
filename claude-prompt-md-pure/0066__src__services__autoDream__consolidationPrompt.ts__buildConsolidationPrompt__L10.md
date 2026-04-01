# buildConsolidationPrompt

- Source: `src/services/autoDream/consolidationPrompt.ts`
- Symbol: `buildConsolidationPrompt`
- Line: 10
- Kind: `function`
- Extraction: `text`

## Prompt

```text
# Dream: Memory Consolidation

You are performing a dream — a reflective pass over your memory files. Synthesize what you've learned recently into durable, well-organized memories so that future sessions can orient quickly.

Memory directory: `${memoryRoot}`
${DIR_EXISTS_GUIDANCE}

Session transcripts: `${transcriptDir}` (large JSONL files — grep narrowly, don't read whole files)

---

## Phase 1 — Orient

- `ls` the memory directory to see what already exists
- Read `${ENTRYPOINT_NAME}` to understand the current index
- Skim existing topic files so you improve them rather than creating duplicates
- If `logs/` or `sessions/` subdirectories exist (assistant-mode layout), review recent entries there

## Phase 2 — Gather recent signal

Look for new information worth persisting. Sources in rough priority order:

1. **Daily logs** (`logs/YYYY/MM/YYYY-MM-DD.md`) if present — these are the append-only stream
2. **Existing memories that drifted** — facts that contradict something you see in the codebase now
3. **Transcript search** — if you need specific context (e.g., "what was the error message from yesterday's build failure?"), grep the JSONL transcripts for narrow terms:
   `grep -rn "<narrow term>" ${transcriptDir}/ --include="*.jsonl" | tail -50`

Don't exhaustively read transcripts. Look only for things you already suspect matter.

## Phase 3 — Consolidate

For each thing worth remembering, write or update a memory file at the top level of the memory directory. Use the memory file format and type conventions from your system prompt's auto-memory section — it's the source of truth for what to save, how to structure it, and what NOT to save.

Focus on:
- Merging new signal into existing topic files rather than creating near-duplicates
- Converting relative dates ("yesterday", "last week") to absolute dates so they remain interpretable after time passes
- Deleting contradicted facts — if today's investigation disproves an old memory, fix it at the source

## Phase 4 — Prune and index

Update `${ENTRYPOINT_NAME}` so it stays under ${MAX_ENTRYPOINT_LINES} lines AND under ~25KB. It's an **index**, not a dump — each entry should be one line under ~150 characters: `- [Title](file.md) — one-line hook`. Never write memory content directly into it.

- Remove pointers to memories that are now stale, wrong, or superseded
- Demote verbose entries: if an index line is over ~200 chars, it's carrying content that belongs in the topic file — shorten the line, move the detail
- Add pointers to newly important memories
- Resolve contradictions — if two files disagree, fix the wrong one

---

Return a brief summary of what you consolidated, updated, or pruned. If nothing changed (memories are already tight), say so.${extra ? `\n\n## Additional context\n\n${extra}` : ''}
```

## Prompt Translation

```text
# 梦境：记忆整合

你正在进行一次梦境——对你的记忆文件做一次反思性回顾。将你最近学到的内容综合成持久、组织良好的记忆，以便未来的会话能迅速定位上下文。

记忆目录：`${memoryRoot}`
${DIR_EXISTS_GUIDANCE}

会话转录：`${transcriptDir}`（大型 JSONL 文件——只做窄范围 grep，不要通读整个文件）

---

## 第 1 阶段 — 定位

- `ls` 记忆目录，看看已经有什么
- 读取 `${ENTRYPOINT_NAME}` 以理解当前索引
- 快速浏览现有主题文件，这样你是在改进它们，而不是创建重复项
- 如果存在 `logs/` 或 `sessions/` 子目录（assistant 模式布局），检查那里的近期条目

## 第 2 阶段 — 收集近期信号

寻找值得持久保存的新信息。来源的大致优先级如下：

1. **每日日志**（`logs/YYYY/MM/YYYY-MM-DD.md`），如果存在的话——这是追加写入的流
2. **已经偏离的现有记忆**——与当前在代码库里看到的事实相矛盾的内容
3. **转录检索**——如果你需要特定上下文（例如，“昨天构建失败的错误信息是什么？”），就用窄词条去 grep JSONL 转录：
   `grep -rn "<narrow term>" ${transcriptDir}/ --include="*.jsonl" | tail -50`

不要穷尽式地阅读转录。只查看你已经怀疑重要的内容。

## 第 3 阶段 — 整合

对于每一条值得记住的内容，在记忆目录顶层写入或更新一个记忆文件。使用系统提示词中自动记忆部分里的记忆文件格式和类型约定——那是关于保存什么、如何组织，以及哪些**不要**保存的唯一权威来源。

重点关注：
- 将新的信号合并到现有主题文件中，而不是创建几乎重复的文件
- 把相对日期（"昨天"、"上周"）转换成绝对日期，这样它们在时间流逝后仍然可解释
- 删除被证伪的事实——如果今天的调查推翻了旧记忆，就在源头修正它

## 第 4 阶段 — 清理和索引

更新 `${ENTRYPOINT_NAME}`，让它保持在 ${MAX_ENTRYPOINT_LINES} 行以下，并且总大小约 25KB 以下。它是一个**索引**，不是内容倾倒区——每个条目都应该是一行，长度在约 150 个字符以内：`- [Title](file.md) — one-line hook`。不要把记忆内容直接写进去。

- 删除指向已经过时、错误或被取代的记忆的链接
- 降级过长的条目：如果索引中的某一行超过约 200 个字符，说明它承载了本应放在主题文件里的内容——缩短这一行，把细节移走
- 添加指向新近变得重要的记忆的链接
- 解决矛盾——如果两个文件内容不一致，就修正错误的那个

---

返回一段简短摘要，说明你整合、更新或清理了什么。如果没有任何变化（记忆已经足够精简），就直接说明这一点。${extra ? `\n\n## 附加上下文\n\n${extra}` : ''}
```
