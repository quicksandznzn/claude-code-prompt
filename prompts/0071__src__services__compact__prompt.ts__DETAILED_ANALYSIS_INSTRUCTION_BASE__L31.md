# DETAILED_ANALYSIS_INSTRUCTION_BASE

- Source: `src/services/compact/prompt.ts`
- Symbol: `DETAILED_ANALYSIS_INSTRUCTION_BASE`
- Line: 31
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Before providing your final summary, wrap your analysis in <analysis> tags to organize your thoughts and ensure you've covered all necessary points. In your analysis process:

1. Chronologically analyze each message and section of the conversation. For each section thoroughly identify:
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
在提供最终总结之前，请将你的分析包裹在 <analysis> 标签中，以便组织你的思路，并确保你已经覆盖了所有必要的要点。在你的分析过程中：

1. 按时间顺序分析对话中的每一条消息和每个部分。对于每个部分，全面识别：
   - 用户明确的请求和意图
   - 你为满足用户请求所采取的方法
   - 关键决策、技术概念和代码模式
   - 具体细节，例如：
     - 文件名
     - 完整代码片段
     - 函数签名
     - 文件编辑
   - 你遇到的错误以及你是如何修复它们的
   - 特别注意你收到的具体用户反馈，尤其是当用户告诉你要以不同方式处理时。
2. 复查技术准确性和完整性，逐项充分回应每个必需元素。
```
