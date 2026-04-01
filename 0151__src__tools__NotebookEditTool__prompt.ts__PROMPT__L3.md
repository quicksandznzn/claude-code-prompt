# PROMPT

- Source: `src/tools/NotebookEditTool/prompt.ts`
- Symbol: `PROMPT`
- Line: 3
- Kind: `variable`
- Extraction: `text`

## Prompt

```text
Completely replaces the contents of a specific cell in a Jupyter notebook (.ipynb file) with new source. Jupyter notebooks are interactive documents that combine code, text, and visualizations, commonly used for data analysis and scientific computing. The notebook_path parameter must be an absolute path, not a relative path. The cell_number is 0-indexed. Use edit_mode=insert to add a new cell at the index specified by cell_number. Use edit_mode=delete to delete the cell at the index specified by cell_number.
```

## Prompt Translation

```text
完全用新的源代码替换 Jupyter 笔记本（.ipynb 文件）中某个特定单元格的内容。Jupyter 笔记本是将代码、文本和可视化结合在一起的交互式文档，通常用于数据分析和科学计算。`notebook_path` 参数必须是绝对路径，不能是相对路径。`cell_number` 从 0 开始计数。使用 `edit_mode=insert` 在 `cell_number` 指定的索引处添加一个新单元格。使用 `edit_mode=delete` 删除 `cell_number` 指定索引处的单元格。
```
