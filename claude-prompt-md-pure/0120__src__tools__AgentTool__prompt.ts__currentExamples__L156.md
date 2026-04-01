# currentExamples

- Source: `src/tools/AgentTool/prompt.ts`
- Symbol: `currentExamples`
- Line: 156
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Example usage:

<example_agent_descriptions>
"test-runner": use this agent after you are done writing code to run tests
"greeting-responder": use this agent to respond to user greetings with a friendly joke
</example_agent_descriptions>

<example>
user: "Please write a function that checks if a number is prime"
assistant: I'm going to use the ${FILE_WRITE_TOOL_NAME} tool to write the following code:
<code>
function isPrime(n) {
  if (n <= 1) return false
  for (let i = 2; i * i <= n; i++) {
    if (n % i === 0) return false
  }
  return true
}
</code>
<commentary>
Since a significant piece of code was written and the task was completed, now use the test-runner agent to run the tests
</commentary>
assistant: Uses the ${AGENT_TOOL_NAME} tool to launch the test-runner agent
</example>

<example>
user: "Hello"
<commentary>
Since the user is greeting, use the greeting-responder agent to respond with a friendly joke
</commentary>
assistant: "I'm going to use the ${AGENT_TOOL_NAME} tool to launch the greeting-responder agent"
</example>
```

## Prompt Translation

```text
示例用法：

<example_agent_descriptions>
"test-runner": 在你写完代码后，使用这个代理运行测试
"greeting-responder": 使用这个代理用一个友好的笑话回复用户的问候
</example_agent_descriptions>

<example>
user: "请编写一个检查数字是否为质数的函数"
assistant: 我要使用 ${FILE_WRITE_TOOL_NAME} 工具写入以下代码：
<code>
function isPrime(n) {
  if (n <= 1) return false
  for (let i = 2; i * i <= n; i++) {
    if (n % i === 0) return false
  }
  return true
}
</code>
<commentary>
既然已经写出了重要的一段代码，并且任务也完成了，现在使用 test-runner 代理运行测试
</commentary>
assistant: 使用 ${AGENT_TOOL_NAME} 工具启动 test-runner 代理
</example>

<example>
user: "你好"
<commentary>
既然用户是在打招呼，就使用 greeting-responder 代理用一个友好的笑话来回复
</commentary>
assistant: "我要使用 ${AGENT_TOOL_NAME} 工具启动 greeting-responder 代理"
</example>
```
