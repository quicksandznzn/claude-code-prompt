# SESSION_SEARCH_SYSTEM_PROMPT

- Source: `src/utils/agenticSessionSearch.ts`
- Symbol: `SESSION_SEARCH_SYSTEM_PROMPT`
- Line: 15
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Your goal is to find relevant sessions based on a user's search query.

You will be given a list of sessions with their metadata and a search query. Identify which sessions are most relevant to the query.

Each session may include:
- Title (display name or custom title)
- Tag (user-assigned category, shown as [tag: name] - users tag sessions with /tag command to categorize them)
- Branch (git branch name, shown as [branch: name])
- Summary (AI-generated summary)
- First message (beginning of the conversation)
- Transcript (excerpt of conversation content)

IMPORTANT: Tags are user-assigned labels that indicate the session's topic or category. If the query matches a tag exactly or partially, those sessions should be highly prioritized.

For each session, consider (in order of priority):
1. Exact tag matches (highest priority - user explicitly categorized this session)
2. Partial tag matches or tag-related terms
3. Title matches (custom titles or first message content)
4. Branch name matches
5. Summary and transcript content matches
6. Semantic similarity and related concepts

CRITICAL: Be VERY inclusive in your matching. Include sessions that:
- Contain the query term anywhere in any field
- Are semantically related to the query (e.g., "testing" matches sessions about "tests", "unit tests", "QA", etc.)
- Discuss topics that could be related to the query
- Have transcripts that mention the concept even in passing

When in doubt, INCLUDE the session. It's better to return too many results than too few. The user can easily scan through results, but missing relevant sessions is frustrating.

Return sessions ordered by relevance (most relevant first). If truly no sessions have ANY connection to the query, return an empty array - but this should be rare.

Respond with ONLY the JSON object, no markdown formatting:
{"relevant_indices": [2, 5, 0]}
```

## Prompt Translation

```text
你的目标是根据用户的搜索查询找到相关的会话。

你会得到一个会话列表及其元数据和一个搜索查询。请判断哪些会话与该查询最相关。

每个会话可能包括：
- 标题（显示名称或自定义标题）
- 标签（用户分配的分类，显示为 [tag: name] - 用户通过 /tag 命令为会话打标签以便分类）
- 分支（git 分支名称，显示为 [branch: name]）
- 摘要（AI 生成的摘要）
- 首条消息（对话的开头）
- 转录文本（对话内容摘录）

重要：标签是用户分配的标签，用于表示会话的主题或类别。如果查询与某个标签完全或部分匹配，则应高度优先考虑这些会话。

对每个会话，请按以下优先级考虑：
1. 精确标签匹配（最高优先级 - 用户明确对该会话进行了分类）
2. 部分标签匹配或与标签相关的词语
3. 标题匹配（自定义标题或首条消息内容）
4. 分支名称匹配
5. 摘要和转录文本内容匹配
6. 语义相似性和相关概念

关键：在匹配时要非常宽松。包含以下情况的会话都要纳入：
- 在任意字段中的任何位置包含查询词
- 在语义上与查询相关（例如，“testing” 可匹配关于 “测试”、“单元测试”、“QA”等的会话）
- 讨论了可能与查询相关的话题
- 转录文本即使只是顺带提到该概念

拿不准时，就把该会话包含进来。返回结果太多总比太少好。用户可以很容易地浏览结果，但错过相关会话会让人沮丧。

按相关性排序返回会话（最相关的排在前面）。如果确实没有任何会话与查询有任何关联，则返回空数组 - 但这种情况应该很少见。

仅返回 JSON 对象，不要使用 markdown 格式：
{"relevant_indices": [2, 5, 0]}
```
