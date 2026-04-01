# WORKER_INSTRUCTIONS

- Source: `src/skills/bundled/batch.ts`
- Symbol: `WORKER_INSTRUCTIONS`
- Line: 12
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
After you finish implementing the change:
1. **Simplify** — Invoke the `${SKILL_TOOL_NAME}` tool with `skill: "simplify"` to review and clean up your changes.
2. **Run unit tests** — Run the project's test suite (check for package.json scripts, Makefile targets, or common commands like `npm test`, `bun test`, `pytest`, `go test`). If tests fail, fix them.
3. **Test end-to-end** — Follow the e2e test recipe from the coordinator's prompt (below). If the recipe says to skip e2e for this unit, skip it.
4. **Commit and push** — Commit all changes with a clear message, push the branch, and create a PR with `gh pr create`. Use a descriptive title. If `gh` is not available or the push fails, note it in your final message.
5. **Report** — End with a single line: `PR: <url>` so the coordinator can track it. If no PR was created, end with `PR: none — <reason>`.
```

## Prompt Translation

```text
在你完成实现该变更后：
1. **简化** — 调用 `${SKILL_TOOL_NAME}` 工具，并使用 `skill: "simplify"` 来审查并清理你的修改。
2. **运行单元测试** — 运行项目的测试套件（检查 `package.json` 脚本、`Makefile` 目标，或常见命令如 `npm test`、`bun test`、`pytest`、`go test`）。如果测试失败，就修复它们。
3. **端到端测试** — 按照协调器提示词中的 e2e 测试流程（见下方）执行。如果该流程说明对这个单元跳过 e2e，就跳过。
4. **提交并推送** — 使用清晰的信息提交所有改动，推送分支，并使用 `gh pr create` 创建 PR。使用描述性的标题。如果 `gh` 不可用或推送失败，请在最终消息中说明。
5. **报告** — 最后一行只写：`PR: <url>`，这样协调器就能跟踪。如果没有创建 PR，最后写：`PR: none — <原因>`。
```
