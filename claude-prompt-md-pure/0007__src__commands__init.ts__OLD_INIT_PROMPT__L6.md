# OLD_INIT_PROMPT

- Source: `src/commands/init.ts`
- Symbol: `OLD_INIT_PROMPT`
- Line: 6
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Please analyze this codebase and create a CLAUDE.md file, which will be given to future instances of Claude Code to operate in this repository.

What to add:
1. Commands that will be commonly used, such as how to build, lint, and run tests. Include the necessary commands to develop in this codebase, such as how to run a single test.
2. High-level code architecture and structure so that future instances can be productive more quickly. Focus on the "big picture" architecture that requires reading multiple files to understand.

Usage notes:
- If there's already a CLAUDE.md, suggest improvements to it.
- When you make the initial CLAUDE.md, do not repeat yourself and do not include obvious instructions like "Provide helpful error messages to users", "Write unit tests for all new utilities", "Never include sensitive information (API keys, tokens) in code or commits".
- Avoid listing every component or file structure that can be easily discovered.
- Don't include generic development practices.
- If there are Cursor rules (in .cursor/rules/ or .cursorrules) or Copilot rules (in .github/copilot-instructions.md), make sure to include the important parts.
- If there is a README.md, make sure to include the important parts.
- Do not make up information such as "Common Development Tasks", "Tips for Development", "Support and Documentation" unless this is expressly included in other files that you read.
- Be sure to prefix the file with the following text:

```

## Prompt Translation

```text
请分析这个代码库并创建一个 `CLAUDE.md` 文件，未来的 Claude Code 实例会借助它在这个仓库中工作。

需要添加的内容：
1. 常用命令，例如如何构建、lint 和运行测试。包括在这个代码库中开发所需的命令，例如如何运行单个测试。
2. 高层次的代码架构和结构，以便未来的实例能更快上手。重点放在需要阅读多个文件才能理解的“大局”架构上。

使用说明：
- 如果已经有 `CLAUDE.md`，请提出改进建议。
- 在你编写初始的 `CLAUDE.md` 时，不要重复自己，也不要加入显而易见的说明，比如“向用户提供有帮助的错误信息”“为所有新工具编写单元测试”“绝不要在代码或提交中包含敏感信息（API 密钥、令牌）”。
- 避免罗列所有可以轻易发现的组件或文件结构。
- 不要包含泛泛的开发实践。
- 如果有 Cursor 规则（位于 `.cursor/rules/` 或 `.cursorrules`）或 Copilot 规则（位于 `.github/copilot-instructions.md`），务必纳入其中的重要内容。
- 如果有 `README.md`，务必纳入其中的重要内容。
- 不要编造诸如“常见开发任务”“开发提示”“支持与文档”之类的信息，除非这些内容明确出现在你读到的其他文件中。
- 务必在文件开头加上以下文本：
```
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.
```
```
