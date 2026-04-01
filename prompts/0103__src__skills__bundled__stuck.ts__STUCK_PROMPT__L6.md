# STUCK_PROMPT

- Source: `src/skills/bundled/stuck.ts`
- Symbol: `STUCK_PROMPT`
- Line: 6
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
# /stuck — diagnose frozen/slow Claude Code sessions

The user thinks another Claude Code session on this machine is frozen, stuck, or very slow. Investigate and post a report to #claude-code-feedback.

## What to look for

Scan for other Claude Code processes (excluding the current one — PID is in `process.pid` but for shell commands just exclude the PID you see running this prompt). Process names are typically `claude` (installed) or `cli` (native dev build).

Signs of a stuck session:
- **High CPU (≥90%) sustained** — likely an infinite loop. Sample twice, 1-2s apart, to confirm it's not a transient spike.
- **Process state `D` (uninterruptible sleep)** — often an I/O hang. The `state` column in `ps` output; first character matters (ignore modifiers like `+`, `s`, `<`).
- **Process state `T` (stopped)** — user probably hit Ctrl+Z by accident.
- **Process state `Z` (zombie)** — parent isn't reaping.
- **Very high RSS (≥4GB)** — possible memory leak making the session sluggish.
- **Stuck child process** — a hung `git`, `node`, or shell subprocess can freeze the parent. Check `pgrep -lP <pid>` for each session.

## Investigation steps

1. **List all Claude Code processes** (macOS/Linux):
   ```
   ps -axo pid=,pcpu=,rss=,etime=,state=,comm=,command= | grep -E '(claude|cli)' | grep -v grep
   ```
   Filter to rows where `comm` is `claude` or (`cli` AND the command path contains "claude").

2. **For anything suspicious**, gather more context:
   - Child processes: `pgrep -lP <pid>`
   - If high CPU: sample again after 1-2s to confirm it's sustained
   - If a child looks hung (e.g., a git command), note its full command line with `ps -p <child_pid> -o command=`
   - Check the session's debug log if you can infer the session ID: `~/.claude/debug/<session-id>.txt` (the last few hundred lines often show what it was doing before hanging)

3. **Consider a stack dump** for a truly frozen process (advanced, optional):
   - macOS: `sample <pid> 3` gives a 3-second native stack sample
   - This is big — only grab it if the process is clearly hung and you want to know *why*

## Report

**Only post to Slack if you actually found something stuck.** If every session looks healthy, tell the user that directly — do not post an all-clear to the channel.

If you did find a stuck/slow session, post to **#claude-code-feedback** (channel ID: `C07VBSHV7EV`) using the Slack MCP tool. Use ToolSearch to find `slack_send_message` if it's not already loaded.

**Use a two-message structure** to keep the channel scannable:

1. **Top-level message** — one short line: hostname, Claude Code version, and a terse symptom (e.g. "session PID 12345 pegged at 100% CPU for 10min" or "git subprocess hung in D state"). No code blocks, no details.
2. **Thread reply** — the full diagnostic dump. Pass the top-level message's `ts` as `thread_ts`. Include:
   - PID, CPU%, RSS, state, uptime, command line, child processes
   - Your diagnosis of what's likely wrong
   - Relevant debug log tail or `sample` output if you captured it

If Slack MCP isn't available, format the report as a message the user can copy-paste into #claude-code-feedback (and let them know to thread the details themselves).

## Notes
- Don't kill or signal any processes — this is diagnostic only.
- If the user gave an argument (e.g., a specific PID or symptom), focus there first.
```

## Prompt Translation

```text
# /stuck — 诊断冻结/缓慢的 Claude Code 会话

用户认为这台机器上的另一个 Claude Code 会话已冻结、卡住或非常慢。请调查并将报告发到 #claude-code-feedback。

## 需要查看什么

扫描其他 Claude Code 进程（排除当前进程——PID 在 `process.pid` 中，但对于 shell 命令，只需排除你看到正在运行此提示的 PID）。进程名通常是 `claude`（已安装版本）或 `cli`（原生开发构建）。

卡住会话的迹象：
- **持续高 CPU（≥90%）** —— 很可能是无限循环。间隔 1-2 秒采样两次，确认不是短暂尖峰。
- **进程状态 `D`（不可中断睡眠）** —— 通常是 I/O 卡住。`ps` 输出中的 `state` 列；首字符最重要（忽略 `+`、`s`、`<` 之类的修饰符）。
- **进程状态 `T`（已停止）** —— 用户可能不小心按了 Ctrl+Z。
- **进程状态 `Z`（僵尸）** —— 父进程没有回收。
- **非常高的 RSS（≥4GB）** —— 可能存在内存泄漏，导致会话变慢。
- **卡住的子进程** —— 挂起的 `git`、`node` 或 shell 子进程可能会冻结父进程。对每个会话检查 `pgrep -lP <pid>`。

## 调查步骤

1. **列出所有 Claude Code 进程**（macOS/Linux）：
   ```
   ps -axo pid=,pcpu=,rss=,etime=,state=,comm=,command= | grep -E '(claude|cli)' | grep -v grep
   ```
   将结果过滤为 `comm` 为 `claude` 的行，或（`cli` 且命令路径包含 `claude`）的行。

2. **对于任何可疑项**，收集更多上下文：
   - 子进程：`pgrep -lP <pid>`
   - 如果 CPU 很高：1-2 秒后再次采样，确认是持续性的
   - 如果某个子进程看起来挂起了（例如 `git` 命令），用 `ps -p <child_pid> -o command=` 记录其完整命令行
   - 如果你能推断出会话 ID，就检查该会话的调试日志：`~/.claude/debug/<session-id>.txt`（最后几百行通常能显示它在卡住前在做什么）

3. **对于真正冻结的进程，可考虑获取堆栈转储**（高级，可选）：
   - macOS：`sample <pid> 3` 会生成 3 秒的原生堆栈采样
   - 这东西很大——只有在进程明显卡死且你想知道 *为什么* 时才获取

## 报告

**只有在你确实发现有卡住的东西时才发到 Slack。** 如果每个会话看起来都正常，直接告诉用户这一点——不要向频道发送一条一切正常的消息。

如果你确实找到了卡住/缓慢的会话，请使用 Slack MCP 工具发到 **#claude-code-feedback**（频道 ID：`C07VBSHV7EV`）。如果尚未加载，使用 ToolSearch 查找 `slack_send_message`。

**使用双消息结构**，以便频道内容便于浏览：

1. **顶层消息** —— 一行简短说明：hostname、Claude Code 版本，以及简洁的症状（例如“会话 PID 12345 持续 10 分钟占满 100% CPU”或“git 子进程卡在 D 状态”）。不要代码块，不要细节。
2. **线程回复** —— 完整的诊断转储。将顶层消息的 `ts` 作为 `thread_ts` 传入。包含：
   - PID、CPU%、RSS、state、运行时长、命令行、子进程
   - 你对最可能问题的诊断
   - 如果你捕获了相关内容，请附上调试日志末尾或 `sample` 输出

如果 Slack MCP 不可用，请将报告整理成用户可以复制粘贴到 #claude-code-feedback 的消息（并告知他们需要自己把细节补到线程里）。

## 备注
- 不要杀死或向任何进程发送信号——这只是诊断。
- 如果用户提供了一个参数（例如特定 PID 或症状），先重点查看那里。
```
