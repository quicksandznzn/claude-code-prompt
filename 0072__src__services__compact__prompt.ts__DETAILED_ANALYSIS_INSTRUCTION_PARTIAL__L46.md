# DETAILED_ANALYSIS_INSTRUCTION_PARTIAL

- Source: `src/services/compact/prompt.ts`
- Symbol: `DETAILED_ANALYSIS_INSTRUCTION_PARTIAL`
- Line: 46
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Before providing your final summary, wrap your analysis in <analysis> tags to organize your thoughts and ensure you've covered all necessary points. In your analysis process:

1. Analyze the recent messages chronologically. For each section thoroughly identify:
   - The user's explicit requests and intents
   - Your approach to addressing the user's requests
   - Key decisions, technical concepts and code patterns
   - Specific details like:
     - file names
     - full code snippets
     - function signatures
     - file edits
   - Errors that you ran into and how you fixed them
   - Pay special attention to specific user feedback that you received, especially if the user told you to do something differently.
2. Double-check for technical accuracy and completeness, addressing each required element thoroughly.
```

## Prompt Translation

```text
在提供最终总结之前，请将你的分析包裹在 <analysis> 标签中，以便组织你的思路，并确保你已经覆盖了所有必要要点。在你的分析过程中：

1. 按时间顺序分析最近的消息。对于每个部分，全面识别：
   - 用户明确提出的请求和意图
   - 你为满足用户请求所采取的方法
   - 关键决策、技术概念和代码模式
   - 具体细节，例如：
     - 文件名
     - 完整代码片段
     - 函数签名
     - 文件修改
   - 你遇到的错误以及你是如何修复它们的
   - 特别关注你收到的具体用户反馈，尤其是当用户告诉你要以不同方式处理时。
2. 再次检查技术准确性和完整性，彻底覆盖每一项必需内容。
```
