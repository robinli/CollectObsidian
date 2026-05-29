# 整理 Clippings 本地命令

此命令用於 Codex Desktop App 本地整理 Obsidian 剪藏。執行時以本文件作為入口，並參考 `.github/agents/knowledge.agent.md` 的內容整理規範。

若本文件與其他專案文件有衝突，以本文件為準。

## 執行目標

將 `Clippings/` 目錄下所有待處理 Markdown 剪藏整理、改名、歸檔至正確目錄，並在完成後輸出處理報告。

## 強制流程

### 1. 處理前建立 commit

在讀取與搬移剪藏前，必須先檢查 git 狀態：

```powershell
git status --short
```

若工作區有任何未提交變更，先向使用者列出變更摘要，然後建立處理前快照 commit。

建議 commit message：

```text
維護：整理剪藏前建立快照
```

若工作區是乾淨的，仍需明確告知使用者「目前無需建立處理前快照 commit」，再繼續整理。

### 2. 讀取整理規則

依序讀取：

1. `.codex/prompts/organize-clippings.md`
2. `.github/agents/knowledge.agent.md`
3. `AI/README.md`
4. `README.md`

使用 `.github/agents/knowledge.agent.md` 的內容整理規則，但目錄策略以本文件為準。

### 3. 掃描所有待處理檔案

掃描：

```text
Clippings/*.md
```

排除：

```text
Clippings/README.md
```

所有非 README 的 Markdown 檔案都視為待處理。一次處理全部待處理檔案，不只處理新增檔，也不只處理單篇。

### 4. 逐篇整理與歸檔

每篇剪藏依序執行：

1. 讀取全文。
2. 判斷內容類型與歸檔目的地。
3. 補齊 YAML frontmatter。
4. 產生繁體中文摘要、重點與可行動事項。
5. 正規化 Markdown 結構。
6. 重新命名為 `YYYY-MM-DD - 中文標題.md`。
7. 將檔案搬離 `Clippings/`。
8. 更新 `00-Home.md`。
9. 若目的地目錄有 `README.md`，更新該 README 的列表。

保留原文重要內容，不得刪除來源脈絡。

### 5. 目錄策略

現階段以既有輕量知識庫結構為準：

```text
AI/
Clippings/
Resources/
Templates/
```

整理後檔案優先歸入 `Resources/` 及其既有或合理子目錄，例如：

```text
Resources/AI/
Resources/Tools/
```

不要自動建立 `Notes/`、`Areas/`、`Archives/` 等 PARA 目錄，除非使用者明確要求。

### 6. 完成後輸出處理報告

整理完成後，必須向使用者列出處理說明，包含：

```markdown
## 處理摘要

共處理 N 篇 Clippings。

| 原始檔案 | 新位置 | 分類理由 |
|----------|--------|----------|
| Clippings/example.md | Resources/AI/YYYY-MM-DD - 標題.md | 分類理由 |

## 更新項目

- 更新 `00-Home.md`
- 更新 `Resources/.../README.md`

## 檢查結果

- `Clippings/` 是否已無待處理 Markdown
- frontmatter 是否已補齊
- tags 是否使用 namespace 格式
- 原文重要內容是否已保留
```

### 7. 處理後不自動 commit

完成整理與報告後，不要自動建立整理 commit。

先停下來讓使用者檢查 diff 與處理報告。只有在使用者明確確認後，才建立處理後 commit。

建議處理後 commit message：

```text
整理：整理 Clippings 剪藏並歸檔
```

## 完成條件

- 已處理 `Clippings/` 下所有非 README Markdown 檔案。
- 所有處理後檔案已搬出 `Clippings/`。
- 已更新必要索引。
- 已輸出處理報告。
- 未經使用者確認，不建立處理後 commit。
