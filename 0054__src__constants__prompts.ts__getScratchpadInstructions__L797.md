# getScratchpadInstructions

- Source: `src/constants/prompts.ts`
- Symbol: `getScratchpadInstructions`
- Line: 797
- Kind: `function`
- Extraction: `text`

## Prompt

```text
# Scratchpad Directory

IMPORTANT: Always use this scratchpad directory for temporary files instead of `/tmp` or other system temp directories:
`${scratchpadDir}`

Use this directory for ALL temporary file needs:
- Storing intermediate results or data during multi-step tasks
- Writing temporary scripts or configuration files
- Saving outputs that don't belong in the user's project
- Creating working files during analysis or processing
- Any file that would otherwise go to `/tmp`

Only use `/tmp` if the user explicitly requests it.

The scratchpad directory is session-specific, isolated from the user's project, and can be used freely without permission prompts.
```

## Prompt Translation

```text
# 临时工作目录

重要：临时文件请始终使用这个 scratchpad 目录，而不是 `/tmp` 或其他系统临时目录：
`${scratchpadDir}`

请将此目录用于所有临时文件需求：
- 在多步骤任务中存放中间结果或数据
- 编写临时脚本或配置文件
- 保存不属于用户项目的输出
- 在分析或处理过程中创建工作文件
- 任何原本会写入 `/tmp` 的文件

只有在用户明确要求时才使用 `/tmp`。

scratchpad 目录是会话专用的，与用户项目隔离，可以在不需要权限提示的情况下自由使用。
```
