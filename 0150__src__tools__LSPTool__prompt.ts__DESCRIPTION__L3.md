# DESCRIPTION

- Source: `src/tools/LSPTool/prompt.ts`
- Symbol: `DESCRIPTION`
- Line: 3
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Interact with Language Server Protocol (LSP) servers to get code intelligence features.

Supported operations:
- goToDefinition: Find where a symbol is defined
- findReferences: Find all references to a symbol
- hover: Get hover information (documentation, type info) for a symbol
- documentSymbol: Get all symbols (functions, classes, variables) in a document
- workspaceSymbol: Search for symbols across the entire workspace
- goToImplementation: Find implementations of an interface or abstract method
- prepareCallHierarchy: Get call hierarchy item at a position (functions/methods)
- incomingCalls: Find all functions/methods that call the function at a position
- outgoingCalls: Find all functions/methods called by the function at a position

All operations require:
- filePath: The file to operate on
- line: The line number (1-based, as shown in editors)
- character: The character offset (1-based, as shown in editors)

Note: LSP servers must be configured for the file type. If no server is available, an error will be returned.
```

## Prompt Translation

```text
与语言服务器协议（LSP）服务器交互，以获取代码智能功能。

支持的操作：
- goToDefinition：查找符号的定义位置
- findReferences：查找某个符号的所有引用
- hover：获取符号的悬停信息（文档、类型信息）
- documentSymbol：获取文档中的所有符号（函数、类、变量）
- workspaceSymbol：在整个工作区中搜索符号
- goToImplementation：查找接口或抽象方法的实现
- prepareCallHierarchy：获取某个位置的调用层级项（函数/方法）
- incomingCalls：查找调用某个位置函数的所有函数/方法
- outgoingCalls：查找由某个位置函数调用的所有函数/方法

所有操作都需要：
- filePath：要操作的文件
- line：行号（从 1 开始，如编辑器所示）
- character：字符偏移量（从 1 开始，如编辑器所示）

注意：LSP 服务器必须为该文件类型进行配置。如果没有可用的服务器，将返回错误。
```
