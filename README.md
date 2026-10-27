# milkup（修改版）

本仓库基于 [Auto-Plugin/milkup](https://github.com/Auto-Plugin/milkup) 修改，原版介绍、功能说明与下载请见原仓库：
https://github.com/Auto-Plugin/milkup

以下只列出本仓库相对原版的改动。

## 改动

### 1. 保存后光标保持在原位

- **原版问题**：保存文档后，光标会自动跳到文档末尾。
- **改动**：保存后回读文件时，编辑器只替换真正有差异的部分；内容没变则不动编辑器，光标位置和撤销历史都会保留。
- **代码**：`src/core/editor.ts` 的 `setMarkdown`。

### 2. 表格单元格内只复制选中的文字

- **原版问题**：在表格单元格里只选中几个字复制时，会把整个单元格的文字都复制出来。
- **改动**：选区在同一个单元格内时，纯文本和富文本都只包含选中的那部分，粘贴到其他应用时也不再带表格外壳。跨多个单元格复制的行为不变，仍按整格复制（同行用 Tab 分隔、同列用换行分隔）。
- **代码**：`src/core/editor.ts` 的 `getSingleTableCellSelectionSlice`、`serializeTableSelectionForClipboard`、`createRichClipboardPayload`。

两项改动的测试见 `test/editor-clipboard.test.mjs`。

## 自行打包（Windows）

需要 Node.js 22+ 和 pnpm：

```bash
pnpm install
pnpm run dist:win-x64
```

安装包输出在 `dist/` 目录。
