# CollectObsidian Clipping Rules

## Goal

Organize every pending Markdown clipping from `Clippings/`, create a clean resource note in the correct `Resources/` destination, archive the original clipping under `Raw/`, update indexes, and report the result.

## Directory Strategy

This repository currently uses a lightweight knowledge base structure:

```text
AI/
Clippings/
Raw/
Resources/
Templates/
```

Processed clippings should usually go under `Resources/` or an existing/reasonable child directory:

```text
Resources/AI/
Resources/Tools/
```

Original source clippings must be moved to `Raw/` after processing. `Raw/` is an archive for traceability, not a normal processing input.

Do not automatically create `Notes/`, `Areas/`, `Archives/`, or other PARA directories unless the user explicitly requests that structure.

## Pre-Processing Git Snapshot

Run:

```powershell
git status --short
```

If there are uncommitted changes, list a concise summary for the user. Create a pre-processing snapshot commit only after the user explicitly confirms it:

```text
維護：整理剪藏前建立快照
```

If the worktree is clean, explicitly tell the user:

```text
目前無需建立處理前快照 commit
```

## File Selection

Scan:

```text
Clippings/*.md
```

Exclude:

```text
Clippings/README.md
```

Every other Markdown file in `Clippings/` is pending and must be processed in the same run.

Do not scan, summarize, index, or reprocess files under `Raw/` unless the user explicitly asks to inspect an archived original clipping.

## Per-File Processing

For each clipping:

1. Read the full file.
2. Determine content type and destination.
3. Complete or repair YAML frontmatter.
4. Generate a Traditional Chinese summary, key points, and action item.
5. Create a concise resource note in the selected `Resources/` destination.
6. Rename the resource note to `YYYY-MM-DD - 中文標題.md`.
7. Move the original clipping file to `Raw/YYYY-MM-DD - 中文標題.md`.
8. Add source traceability in the resource note, including original URL and a link to the archived raw clipping when useful.
9. Note the destination README that must be updated, if the destination directory has `README.md`.

After all clippings are processed, update `00-Home.md` once and update each affected destination `README.md` once.

Do not delete original clipping files. Keep formal resource notes readable and concise; avoid embedding the full original article because the raw clipping is archived under `Raw/`.

## Destination Guidance

| Content Type | Destination |
|---|---|
| AI tools, AI workflows, model usage, prompt engineering | `Resources/AI/` |
| Tool introductions, software reviews, CLI/app usage | `Resources/Tools/` |
| General reference that does not fit existing categories | `Resources/` |

Prefer existing directories: `Resources/AI/`, `Resources/Tools/`, or `Resources/`. Create a new `Resources/<Topic>/` only when the topic already has multiple related clippings, the category is clear and likely to remain useful, or the user explicitly requests that subdirectory.

## Frontmatter Schema

Ensure each processed clipping has YAML frontmatter with at least:

```yaml
---
title: ""
date: ""
source: ""
raw: ""
author: ""
published: ""
category: ""
tags:
  - type/clipping
  - status/processed
summary: ""
key_points:
  - ""
actionable: ""
---
```

Rules:

- `title`: concise Traditional Chinese title, preferably no more than 30 characters.
- `date`: collection date in `YYYY-MM-DD`; if only `created` exists, migrate it to `date`.
- `raw`: wiki link or relative path to the archived original clipping under `Raw/`; leave empty only if no raw archive exists.
- `source`, `author`, `published`: preserve valid existing values. Leave unknown values empty. Use `待確認` only when the source content explicitly indicates uncertainty.
- `category`: destination path or category name.
- `tags`: use namespace format; remove non-namespace tags unless they are intentionally retained by project convention.
- `summary`: one Traditional Chinese sentence, preferably no more than 50 characters.
- `key_points`: 3 to 5 points, each concise and traceable to the source.
- `actionable`: one concrete action or insight.

## Markdown Body Layout

Use one H1 matching the frontmatter title.

```markdown
# 中文標題

## 摘要

> AI 生成的 2-3 句話摘要

## 重點

- 重點 1
- 重點 2
- 重點 3

## 可行動事項

- [ ] 具體可採取的行動或啟發

## 筆記

整理後的重點脈絡與必要引用，不貼入完整原文。

## 相關筆記

- [[相關筆記]]

## 來源

- 原文：[標題](URL)
- 原始剪藏：[[YYYY-MM-DD - 中文標題]]
- 作者：[[作者名]]
```

Use Traditional Chinese for generated content. Keep technical terms such as API, Git, TDD, CLI, and model names when appropriate. In `筆記`, preserve the source's important context, remove noise, convert Simplified Chinese to Traditional Chinese when needed, and keep the resource note focused. Do not expand the clipping into a longer secondary article and do not paste the full original content; the full original remains in `Raw/`.

## Filename Rules

Use:

```text
YYYY-MM-DD - 中文標題.md
```

Use the same filename for the resource note and the archived raw clipping, placed in different directories.

Remove non-standard prefixes such as `R-`. Remove invalid filename characters:

```text
? * : < > | " / \
```

## Completion Report

After processing, report:

```markdown
## 處理摘要

共處理 N 篇 Clippings。

| 原始檔案 | 整理筆記 | Raw 封存 | 分類理由 |
|----------|----------|----------|----------|
| Clippings/example.md | Resources/AI/YYYY-MM-DD - 標題.md | Raw/YYYY-MM-DD - 標題.md | 分類理由 |

## 更新項目

- 更新 `00-Home.md`
- 更新 `Resources/.../README.md`

## 檢查結果

- `Clippings/` 是否已無待處理 Markdown
- 原始 clipping 是否已移到 `Raw/`
- frontmatter 是否已補齊
- tags 是否使用 namespace 格式
- 整理筆記是否保留來源連結與 Raw 封存連結

## 效率追蹤

- 處理的 clipping 數量
- 更新的索引檔案
- 是否讀取額外既有筆記或其他 repo 文件
```

Do not create the post-processing commit until the user explicitly confirms.

Suggested post-processing commit message:

```text
整理：整理 Clippings 剪藏並歸檔
```
