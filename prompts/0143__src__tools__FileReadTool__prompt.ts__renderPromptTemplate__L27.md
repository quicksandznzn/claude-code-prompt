# renderPromptTemplate

- Source: `src/tools/FileReadTool/prompt.ts`
- Symbol: `renderPromptTemplate`
- Line: 27
- Kind: `function`
- Extraction: `text`

## Prompt

```text
Reads a file from the local filesystem. You can access any file directly by using this tool.
Assume this tool is able to read all files on the machine. If the User provides a path to a file assume that path is valid. It is okay to read a file that does not exist; an error will be returned.

Usage:
- The file_path parameter must be an absolute path, not a relative path
- By default, it reads up to ${MAX_LINES_TO_READ} lines starting from the beginning of the file${maxSizeInstruction}
${offsetInstruction}
${lineFormat}
- This tool allows Claude Code to read images (eg PNG, JPG, etc). When reading an image file the contents are presented visually as Claude Code is a multimodal LLM.${isPDFSupported()
      ? '\n- This tool can read PDF files (.pdf). For large PDFs (more than 10 pages), you MUST provide the pages parameter to read specific page ranges (e.g., pages: "1-5"). Reading a large PDF without the pages parameter will fail. Maximum 20 pages per request.'
      : ''}
- This tool can read Jupyter notebooks (.ipynb files) and returns all cells with their outputs, combining code, text, and visualizations.
- This tool can only read files, not directories. To read a directory, use an ls command via the ${BASH_TOOL_NAME} tool.
- You will regularly be asked to read screenshots. If the user provides a path to a screenshot, ALWAYS use this tool to view the file at the path. This tool will work with all temporary file paths.
- If you read a file that exists but has empty contents you will receive a system reminder warning in place of file contents.
```

## Prompt Translation

```text
从本地文件系统读取文件。你可以直接使用此工具访问任意文件。
假定此工具能够读取机器上的所有文件。如果用户提供了某个文件的路径，则应视为该路径有效。读取不存在的文件也可以；系统会返回错误。

用法：
- file_path 参数必须是绝对路径，不能是相对路径
- 默认情况下，它会从文件开头开始读取最多 ${MAX_LINES_TO_READ} 行${maxSizeInstruction}
${offsetInstruction}
${lineFormat}
- 此工具允许 Claude Code 读取图像（例如 PNG、JPG 等）。在读取图像文件时，内容会以视觉形式呈现，因为 Claude Code 是一个多模态 LLM。${isPDFSupported()
      ? '\n- 此工具可以读取 PDF 文件（.pdf）。对于较大的 PDF（超过 10 页），你必须提供 pages 参数来读取指定的页范围（例如，pages: "1-5"）。不提供 pages 参数读取大型 PDF 会失败。每次请求最多 20 页。'
      : ''}
- 此工具可以读取 Jupyter 笔记本（.ipynb 文件），并返回所有单元及其输出，将代码、文本和可视化内容合并呈现。
- 此工具只能读取文件，不能读取目录。要读取目录，请通过 ${BASH_TOOL_NAME} 工具使用 ls 命令。
- 你会经常被要求读取截图。如果用户提供的是截图路径，务必使用此工具查看该路径下的文件。此工具对所有临时文件路径都有效。
- 如果你读取的是一个存在但内容为空的文件，你会收到一条系统提醒警告，而不是文件内容。
```
