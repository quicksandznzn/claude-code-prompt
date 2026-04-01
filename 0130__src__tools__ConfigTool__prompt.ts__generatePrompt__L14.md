# generatePrompt

- Source: `src/tools/ConfigTool/prompt.ts`
- Symbol: `generatePrompt`
- Line: 14
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Get or set Claude Code configuration settings.

  View or change Claude Code settings. Use when the user requests configuration changes, asks about current settings, or when adjusting a setting would benefit them.


## Usage
- **Get current value:** Omit the "value" parameter
- **Set new value:** Include the "value" parameter

## Configurable settings list
The following settings are available for you to change:

### Global Settings (stored in ~/.claude.json)
${globalSettings.join('\n')}

### Project Settings (stored in settings.json)
${projectSettings.join('\n')}

${modelSection}
## Examples
- Get theme: { "setting": "theme" }
- Set dark theme: { "setting": "theme", "value": "dark" }
- Enable vim mode: { "setting": "editorMode", "value": "vim" }
- Enable verbose: { "setting": "verbose", "value": true }
- Change model: { "setting": "model", "value": "opus" }
- Change permission mode: { "setting": "permissions.defaultMode", "value": "plan" }
```

## Prompt Translation

```text
获取或设置 Claude Code 配置设置。

  查看或更改 Claude Code 设置。当用户请求配置更改、询问当前设置，或者调整某项设置会对他们有帮助时使用。


## 用法
- **获取当前值：** 省略 `value` 参数
- **设置新值：** 包含 `value` 参数

## 可配置设置列表
以下设置可供你更改：

### 全局设置（存储在 ~/.claude.json 中）
${globalSettings.join('\n')}

### 项目设置（存储在 settings.json 中）
${projectSettings.join('\n')}

${modelSection}
## 示例
- 获取主题：{ "setting": "theme" }
- 设置深色主题：{ "setting": "theme", "value": "dark" }
- 启用 vim 模式：{ "setting": "editorMode", "value": "vim" }
- 启用详细输出：{ "setting": "verbose", "value": true }
- 更改模型：{ "setting": "model", "value": "opus" }
- 更改权限模式：{ "setting": "permissions.defaultMode", "value": "plan" }
```
