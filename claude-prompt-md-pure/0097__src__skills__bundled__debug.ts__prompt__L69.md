# prompt

- Source: `src/skills/bundled/debug.ts`
- Symbol: `prompt`
- Line: 69
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
# Debug Skill

Help the user debug an issue they're encountering in this current Claude Code session.
${justEnabledSection}
## Session Debug Log

The debug log for the current session is at: `${debugLogPath}`

${logInfo}

For additional context, grep for [ERROR] and [WARN] lines across the full file.

## Issue Description

${args || 'The user did not describe a specific issue. Read the debug log and summarize any errors, warnings, or notable issues.'}

## Settings

Remember that settings are in:
* user - ${getSettingsFilePathForSource('userSettings')}
* project - ${getSettingsFilePathForSource('projectSettings')}
* local - ${getSettingsFilePathForSource('localSettings')}

## Instructions

1. Review the user's issue description
2. The last ${DEFAULT_DEBUG_LINES_READ} lines show the debug file format. Look for [ERROR] and [WARN] entries, stack traces, and failure patterns across the file
3. Consider launching the ${CLAUDE_CODE_GUIDE_AGENT_TYPE} subagent to understand the relevant Claude Code features
4. Explain what you found in plain language
5. Suggest concrete fixes or next steps
```

## Prompt Translation

```text
# 调试技能

帮助用户调试他们在当前 Claude Code 会话中遇到的问题。
${justEnabledSection}
## 会话调试日志

当前会话的调试日志位于：`${debugLogPath}`

${logInfo}

如需更多上下文，请在整个文件中 grep [ERROR] 和 [WARN] 行。

## 问题描述

${args || '用户没有描述具体问题。请阅读调试日志，并总结任何错误、警告或值得注意的问题。'}

## 设置

请记住，设置位于：
* user - ${getSettingsFilePathForSource('userSettings')}
* project - ${getSettingsFilePathForSource('projectSettings')}
* local - ${getSettingsFilePathForSource('localSettings')}

## 指令

1. 查看用户的问题描述
2. 最后的 ${DEFAULT_DEBUG_LINES_READ} 行展示了调试文件格式。查找整个文件中的 [ERROR] 和 [WARN] 条目、堆栈跟踪以及失败模式
3. 考虑启动 ${CLAUDE_CODE_GUIDE_AGENT_TYPE} 子代理，以了解相关的 Claude Code 功能
4. 用通俗语言解释你发现的内容
5. 提出具体的修复方案或下一步操作
```
