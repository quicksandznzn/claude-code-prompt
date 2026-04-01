# getSimpleSandboxSection

- Source: `src/tools/BashTool/prompt.ts`
- Symbol: `getSimpleSandboxSection`
- Line: 172
- Kind: `function`
- Extraction: `source`

## Source

```ts
function getSimpleSandboxSection(): string {
  if (!SandboxManager.isSandboxingEnabled()) {
    return ''
  }

  const fsReadConfig = SandboxManager.getFsReadConfig()
  const fsWriteConfig = SandboxManager.getFsWriteConfig()
  const networkRestrictionConfig = SandboxManager.getNetworkRestrictionConfig()
  const allowUnixSockets = SandboxManager.getAllowUnixSockets()
  const ignoreViolations = SandboxManager.getIgnoreViolations()
  const allowUnsandboxedCommands =
    SandboxManager.areUnsandboxedCommandsAllowed()

  // Replace the per-UID temp dir literal (e.g. /private/tmp/claude-1001/) with
  // "$TMPDIR" so the prompt is identical across users — avoids busting the
  // cross-user global prompt cache. The sandbox already sets $TMPDIR at runtime.
  const claudeTempDir = getClaudeTempDir()
  const normalizeAllowOnly = (paths: string[]): string[] =>
    [...new Set(paths)].map(p => (p === claudeTempDir ? '$TMPDIR' : p))

  const filesystemConfig = {
    read: {
      denyOnly: dedup(fsReadConfig.denyOnly),
      ...(fsReadConfig.allowWithinDeny && {
        allowWithinDeny: dedup(fsReadConfig.allowWithinDeny),
      }),
    },
    write: {
      allowOnly: normalizeAllowOnly(fsWriteConfig.allowOnly),
      denyWithinAllow: dedup(fsWriteConfig.denyWithinAllow),
    },
  }

  const networkConfig = {
    ...(networkRestrictionConfig?.allowedHosts && {
      allowedHosts: dedup(networkRestrictionConfig.allowedHosts),
    }),
    ...(networkRestrictionConfig?.deniedHosts && {
      deniedHosts: dedup(networkRestrictionConfig.deniedHosts),
    }),
    ...(allowUnixSockets && { allowUnixSockets: dedup(allowUnixSockets) }),
  }

  const restrictionsLines = []
  if (Object.keys(filesystemConfig).length > 0) {
    restrictionsLines.push(`Filesystem: ${jsonStringify(filesystemConfig)}`)
  }
  if (Object.keys(networkConfig).length > 0) {
    restrictionsLines.push(`Network: ${jsonStringify(networkConfig)}`)
  }
  if (ignoreViolations) {
    restrictionsLines.push(
      `Ignored violations: ${jsonStringify(ignoreViolations)}`,
    )
  }

  const sandboxOverrideItems: Array<string | string[]> =
    allowUnsandboxedCommands
      ? [
          'You should always default to running commands within the sandbox. Do NOT attempt to set `dangerouslyDisableSandbox: true` unless:',
          [
            'The user *explicitly* asks you to bypass sandbox',
            'A specific command just failed and you see evidence of sandbox restrictions causing the failure. Note that commands can fail for many reasons unrelated to the sandbox (missing files, wrong arguments, network issues, etc.).',
          ],
          'Evidence of sandbox-caused failures includes:',
          [
            '"Operation not permitted" errors for file/network operations',
            'Access denied to specific paths outside allowed directories',
            'Network connection failures to non-whitelisted hosts',
            'Unix socket connection errors',
          ],
          'When you see evidence of sandbox-caused failure:',
          [
            "Immediately retry with `dangerouslyDisableSandbox: true` (don't ask, just do it)",
            'Briefly explain what sandbox restriction likely caused the failure. Be sure to mention that the user can use the `/sandbox` command to manage restrictions.',
            'This will prompt the user for permission',
          ],
          'Treat each command you execute with `dangerouslyDisableSandbox: true` individually. Even if you have recently run a command with this setting, you should default to running future commands within the sandbox.',
          'Do not suggest adding sensitive paths like ~/.bashrc, ~/.zshrc, ~/.ssh/*, or credential files to the sandbox allowlist.',
        ]
      : [
          'All commands MUST run in sandbox mode - the `dangerouslyDisableSandbox` parameter is disabled by policy.',
          'Commands cannot run outside the sandbox under any circumstances.',
          'If a command fails due to sandbox restrictions, work with the user to adjust sandbox settings instead.',
        ]

  const items: Array<string | string[]> = [
    ...sandboxOverrideItems,
    'For temporary files, always use the `$TMPDIR` environment variable. TMPDIR is automatically set to the correct sandbox-writable directory in sandbox mode. Do NOT use `/tmp` directly - use `$TMPDIR` instead.',
  ]

  return [
    '',
    '## Command sandbox',
    'By default, your command will be run in a sandbox. This sandbox controls which directories and network hosts commands may access or modify without an explicit override.',
    '',
    'The sandbox has the following restrictions:',
    restrictionsLines.join('\n'),
    '',
    ...prependBullets(items),
  ].join('\n')
}
```

## Prompt Translation

```text

## 命令沙箱
默认情况下，你的命令会在沙箱中运行。这个沙箱决定命令在没有显式覆盖时可以访问或修改哪些目录和网络主机。

沙箱有以下限制：
文件系统：${jsonStringify(filesystemConfig)}
网络：${jsonStringify(networkConfig)}
已忽略的违规项：${jsonStringify(ignoreViolations)}

 - 你应始终默认在沙箱内运行命令。不要尝试设置 `dangerouslyDisableSandbox: true`，除非满足以下条件之一：
  - 用户*明确*要求你绕过沙箱
  - 某个具体命令刚刚失败，而且你看到了沙箱限制导致失败的证据。注意，命令失败的原因很多，并不一定和沙箱有关（缺少文件、参数错误、网络问题等）。
 - 沙箱导致失败的证据包括：
  - 文件/网络操作出现 “Operation not permitted” 错误
  - 对允许目录之外的特定路径访问被拒绝
  - 连接未列入白名单的主机时出现网络连接失败
  - Unix socket 连接错误
 - 当你看到沙箱导致失败的证据时：
  - 立即使用 `dangerouslyDisableSandbox: true` 重试（不要询问，直接执行）
  - 简要说明最有可能导致失败的是哪条沙箱限制。务必提到用户可以使用 `/sandbox` 命令来管理这些限制。
  - 这会提示用户授予权限
 - 对每个使用 `dangerouslyDisableSandbox: true` 执行的命令都要单独处理。即使你最近刚用过这个设置，后续命令也仍应默认在沙箱内运行。
 - 不要建议将诸如 `~/.bashrc`、`~/.zshrc`、`~/.ssh/*` 或凭据文件之类的敏感路径加入沙箱白名单。
 - 对于临时文件，始终使用 `$TMPDIR` 环境变量。`TMPDIR` 会在沙箱模式下自动设置为正确的沙箱可写目录。不要直接使用 `/tmp`，而是使用 `$TMPDIR`。
```
