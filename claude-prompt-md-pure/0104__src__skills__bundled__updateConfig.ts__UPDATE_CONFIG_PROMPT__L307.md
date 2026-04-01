# UPDATE_CONFIG_PROMPT

- Source: `src/skills/bundled/updateConfig.ts`
- Symbol: `UPDATE_CONFIG_PROMPT`
- Line: 307
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
# Update Config Skill

Modify Claude Code configuration by updating settings.json files.

## When Hooks Are Required (Not Memory)

If the user wants something to happen automatically in response to an EVENT, they need a **hook** configured in settings.json. Memory/preferences cannot trigger automated actions.

**These require hooks:**
- "Before compacting, ask me what to preserve" → PreCompact hook
- "After writing files, run prettier" → PostToolUse hook with Write|Edit matcher
- "When I run bash commands, log them" → PreToolUse hook with Bash matcher
- "Always run tests after code changes" → PostToolUse hook

**Hook events:** PreToolUse, PostToolUse, PreCompact, PostCompact, Stop, Notification, SessionStart

## CRITICAL: Read Before Write

**Always read the existing settings file before making changes.** Merge new settings with existing ones - never replace the entire file.

## CRITICAL: Use AskUserQuestion for Ambiguity

When the user's request is ambiguous, use AskUserQuestion to clarify:
- Which settings file to modify (user/project/local)
- Whether to add to existing arrays or replace them
- Specific values when multiple options exist

## Decision: Config Tool vs Direct Edit

**Use the Config tool** for these simple settings:
- `theme`, `editorMode`, `verbose`, `model`
- `language`, `alwaysThinkingEnabled`
- `permissions.defaultMode`

**Edit settings.json directly** for:
- Hooks (PreToolUse, PostToolUse, etc.)
- Complex permission rules (allow/deny arrays)
- Environment variables
- MCP server configuration
- Plugin configuration

## Workflow

1. **Clarify intent** - Ask if the request is ambiguous
2. **Read existing file** - Use Read tool on the target settings file
3. **Merge carefully** - Preserve existing settings, especially arrays
4. **Edit file** - Use Edit tool (if file doesn't exist, ask user to create it first)
5. **Confirm** - Tell user what was changed

## Merging Arrays (Important!)

When adding to permission arrays or hook arrays, **merge with existing**, don't replace:

**WRONG** (replaces existing permissions):
```json
{ "permissions": { "allow": ["Bash(npm:*)"] } }
```

## Prompt Translation

```text
# 更新配置技能

通过更新 `settings.json` 文件来修改 Claude Code 配置。

## 何时需要 Hook（不是 Memory）

如果用户希望某件事在响应某个 EVENT 时自动发生，他们需要在 `settings.json` 中配置一个 **hook**。Memory/偏好设置不能触发自动操作。

**这些情况需要 hooks：**
- “在压缩前，问我想保留什么” → PreCompact hook
- “写入文件后，运行 prettier” → 带有 Write|Edit matcher 的 PostToolUse hook
- “当我运行 bash 命令时，记录它们” → 带有 Bash matcher 的 PreToolUse hook
- “在代码变更后总是运行测试” → PostToolUse hook

**Hook 事件：** PreToolUse, PostToolUse, PreCompact, PostCompact, Stop, Notification, SessionStart

## 关键：先读后写

**在进行任何更改之前，始终先读取现有的 settings 文件。** 将新设置与现有设置合并，不要直接替换整个文件。

## 关键：遇到歧义时使用 AskUserQuestion

当用户的请求有歧义时，使用 AskUserQuestion 进行澄清：
- 要修改哪个 settings 文件（user/project/local）
- 是追加到现有数组还是替换它们
- 当存在多个选项时，具体取值是什么

## 决策：Config 工具 vs 直接编辑

**对这些简单设置使用 Config 工具：**
- `theme`, `editorMode`, `verbose`, `model`
- `language`, `alwaysThinkingEnabled`
- `permissions.defaultMode`

**直接编辑 `settings.json` 适用于：**
- Hooks（PreToolUse、PostToolUse 等）
- 复杂的权限规则（allow/deny 数组）
- 环境变量
- MCP server 配置
- Plugin 配置

## 工作流程

1. **澄清意图** - 如果请求有歧义就先询问
2. **读取现有文件** - 对目标 settings 文件使用 Read 工具
3. **谨慎合并** - 保留现有设置，尤其是数组
4. **编辑文件** - 使用 Edit 工具（如果文件不存在，先让用户创建它）
5. **确认** - 告诉用户已更改了什么

## 合并数组（重要！）

在向权限数组或 hook 数组中添加内容时，**要与现有内容合并**，不要替换：

**错误**（会替换现有权限）：
```json
{ "permissions": { "allow": ["Bash(npm:*)"] } }
```

**RIGHT** (preserves existing + adds new):
```json
{
  "permissions": {
    "allow": [
      "Bash(git:*)",      // existing
      "Edit(.claude)",    // existing
      "Bash(npm:*)"       // new
    ]
  }
}
```

${SETTINGS_EXAMPLES_DOCS}

${HOOKS_DOCS}

${HOOK_VERIFICATION_FLOW}

## Example Workflows

### Adding a Hook

User: "Format my code after Claude writes it"

1. **Clarify**: Which formatter? (prettier, gofmt, etc.)
2. **Read**: `.claude/settings.json` (or create if missing)
3. **Merge**: Add to existing hooks, don't replace
4. **Result**:
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write|Edit",
      "hooks": [{
        "type": "command",
        "command": "jq -r '.tool_response.filePath // .tool_input.file_path' | { read -r f; prettier --write \"$f\"; } 2>/dev/null || true"
      }]
    }]
  }
}
```

### Adding Permissions

User: "Allow npm commands without prompting"

1. **Read**: Existing permissions
2. **Merge**: Add `Bash(npm:*)` to allow array
3. **Result**: Combined with existing allows

### Environment Variables

User: "Set DEBUG=true"

1. **Decide**: User settings (global) or project settings?
2. **Read**: Target file
3. **Merge**: Add to env object
```json
{ "env": { "DEBUG": "true" } }
```

## Common Mistakes to Avoid

1. **Replacing instead of merging** - Always preserve existing settings
2. **Wrong file** - Ask user if scope is unclear
3. **Invalid JSON** - Validate syntax after changes
4. **Forgetting to read first** - Always read before write

## Troubleshooting Hooks

If a hook isn't running:
1. **Check the settings file** - Read ~/.claude/settings.json or .claude/settings.json
2. **Verify JSON syntax** - Invalid JSON silently fails
3. **Check the matcher** - Does it match the tool name? (e.g., "Bash", "Write", "Edit")
4. **Check hook type** - Is it "command", "prompt", or "agent"?
5. **Test the command** - Run the hook command manually to see if it works
6. **Use --debug** - Run `claude --debug` to see hook execution logs
```
