# buildMagicDocsUpdatePrompt

- Source: `src/services/MagicDocs/prompts.ts`
- Symbol: `buildMagicDocsUpdatePrompt`
- Line: 98
- Kind: `function`
- Extraction: `source`

## Source

```ts
export async function buildMagicDocsUpdatePrompt(
  docContents: string,
  docPath: string,
  docTitle: string,
  instructions?: string,
): Promise<string> {
  const promptTemplate = await loadMagicDocsPrompt()

  // Build custom instructions section if provided
  const customInstructions = instructions
    ? `

DOCUMENT-SPECIFIC UPDATE INSTRUCTIONS:
The document author has provided specific instructions for how this file should be updated. Pay extra attention to these instructions and follow them carefully:

"${instructions}"

These instructions take priority over the general rules below. Make sure your updates align with these specific guidelines.`
    : ''

  // Substitute variables in the prompt
  const variables = {
    docContents,
    docPath,
    docTitle,
    customInstructions,
  }

  return substituteVariables(promptTemplate, variables)
}
```

## Prompt Translation

```text
重要：这条消息和这些说明并不是实际用户对话的一部分。不要在文档内容中提及“文档更新”、“Magic Docs”或这些更新说明。

基于上面的用户对话（不包括这条文档更新说明消息），更新 Magic Doc 文件，把任何值得保留的新发现、洞见或信息整合进去。

文件 {{docPath}} 已经为你读过。以下是它当前的内容：
<current_doc_content>
{{docContents}}
</current_doc_content>

文档标题：{{docTitle}}
{{customInstructions}}

你的唯一任务是：如果有实质性的新信息需要添加，就使用 Edit 工具更新文档文件，然后停止。你可以进行多次编辑（按需更新多个部分）- 请在同一条消息中并行调用所有 Edit 工具。如果没有实质性的新内容可添加，只需简要说明，不要调用任何工具。

编辑的关键规则：
- 请严格按原样保留 Magic Doc 标题：# MAGIC DOC: {{docTitle}}
- 如果标题后紧跟一行斜体文本，请原样保留
- 保持文档始终与代码库的最新状态一致 - 这不是变更日志，也不是历史记录
- 直接原地更新信息以反映当前状态 - 不要附加历史备注，也不要随时间追踪变更
- 与其添加“之前...”或“更新为...”之类的说明，不如删除或替换过时信息
- 清理或删除不再相关、或与文档目的不一致的部分
- 修正明显错误：拼写错误、语法错误、格式损坏、信息不正确或令人困惑的表述
- 保持文档组织良好：使用清晰的标题、合理的章节顺序、一致的格式和正确的嵌套

文档编写原则 - 仔细阅读：
- 要简洁。只保留高信号内容。不要有冗余内容，也不要不必要地展开
- 文档用于概览、架构和入口点 - 不是详细的代码讲解
- 不要重复从源码本身就能看出的信息
- 不要记录每个函数、参数或行号引用
- 关注：为什么存在、组件如何连接、从哪里开始阅读、使用了什么模式
- 跳过：详细实现步骤、详尽的 API 文档、逐步叙述

应当记录的内容：
- 高层架构和系统设计
- 不明显的模式、约定或坑点
- 关键入口点以及从哪里开始阅读代码
- 重要设计决策及其原因
- 关键依赖或集成点
- 相关文件、文档或代码的引用（像维基一样）- 帮助读者导航到相关上下文

不应记录的内容：
- 从代码本身一眼就能看出的任何内容
- 文件、函数或参数的穷举列表
- 逐步实现细节
- 底层代码机制
- CLAUDE.md 或其他项目文档里已有的信息

使用 Edit 工具，file_path: {{docPath}}

请记住：只有在有实质性的新信息时才更新。Magic Doc 标题（# MAGIC DOC: {{docTitle}}）必须保持不变。
```
