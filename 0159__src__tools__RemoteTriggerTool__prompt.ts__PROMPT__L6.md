# PROMPT

- Source: `src/tools/RemoteTriggerTool/prompt.ts`
- Symbol: `PROMPT`
- Line: 6
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Call the claude.ai remote-trigger API. Use this instead of curl — the OAuth token is added automatically in-process and never exposed.

Actions:
- list: GET /v1/code/triggers
- get: GET /v1/code/triggers/{trigger_id}
- create: POST /v1/code/triggers (requires body)
- update: POST /v1/code/triggers/{trigger_id} (requires body, partial update)
- run: POST /v1/code/triggers/{trigger_id}/run

The response is the raw JSON from the API.
```

## Prompt Translation

```text
调用 claude.ai remote-trigger API。请用它代替 `curl` —— OAuth token 会在进程内自动添加，且不会暴露。

操作：
- 列出: GET /v1/code/triggers
- 获取: GET /v1/code/triggers/{trigger_id}
- 创建: POST /v1/code/triggers (需要 body)
- 更新: POST /v1/code/triggers/{trigger_id} (需要 body，部分更新)
- 运行: POST /v1/code/triggers/{trigger_id}/run

响应是 API 返回的原始 JSON。
```
