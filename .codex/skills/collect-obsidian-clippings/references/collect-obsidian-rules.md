# CollectObsidian Clipping Rules

## Goal

Organize every pending Markdown clipping from `Clippings/`, rename it, move it to the correct `Resources/` destination, update indexes, and report the result.

## Directory Strategy

This repository currently uses a lightweight knowledge base structure:

```text
AI/
Clippings/
Resources/
Templates/
```

Processed clippings should usually go under `Resources/` or an existing/reasonable child directory:

```text
Resources/AI/
Resources/Tools/
```

Do not automatically create `Notes/`, `Areas/`, `Archives/`, or other PARA directories unless the user explicitly requests that structure.

## Pre-Processing Git Snapshot

Run:

```powershell
git status --short
```

If there are uncommitted changes, list a concise summary for the user, then create a pre-processing snapshot commit:

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

## Per-File Processing

For each clipping:

1. Read the full file.
2. Determine content type and destination.
3. Complete or repair YAML frontmatter.
4. Generate a Traditional Chinese summary, key points, and action item.
5. Normalize Markdown structure.
6. Rename to `YYYY-MM-DD - 中文標題.md`.
7. Move the file out of `Clippings/`.
8. Update `00-Home.md`.
9. If the destination directory has `README.md`, update its listing.

Preserve important source context. Do not remove the original article's useful content.

## Destination Guidance

| Content Type | Destination |
|---|---|
| AI tools, AI workflows, model usage, prompt engineering | `Resources/AI/` |
| Tool introductions, software reviews, CLI/app usage | `Resources/Tools/` |
| General reference that does not fit existing categories | `Resources/` or a reasonable child under `Resources/` |

Prefer existing directories. Create a new `Resources/<Topic>/` only when it is clearly useful and consistent with the lightweight structure.

## Frontmatter Schema

Ensure each processed clipping has YAML frontmatter with at least:

```yaml
---
title: ""
date: ""
source: ""
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
- `source`, `author`, `published`: preserve valid existing values; leave empty or mark `待確認` only when the source content supports uncertainty.
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

## 原文整理

整理後的原文內容，保留重要脈絡並改善可讀性。

## 相關筆記

- [[相關筆記]]

## 來源

- 原文：[標題](URL)
- 作者：[[作者名]]
```

Use Traditional Chinese for generated content. Keep technical terms such as API, Git, TDD, CLI, and model names when appropriate.

## Filename Rules

Use:

```text
YYYY-MM-DD - 中文標題.md
```

Remove non-standard prefixes such as `R-`. Remove invalid filename characters:

```text
? * : < > | " / \
```

## Completion Report

After processing, report:

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

Do not create the post-processing commit until the user explicitly confirms.

Suggested post-processing commit message:

```text
整理：整理 Clippings 剪藏並歸檔
```
