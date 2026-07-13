---
name: collect-obsidian-clippings
description: Use when working inside the CollectObsidian repository and the user asks to organize, process, summarize, classify, archive, or clean up Obsidian Clippings markdown files from the Clippings directory.
---

# Collect Obsidian Clippings

## Overview

Use this project skill to process this repository's Obsidian Web Clipper inbox. The source of truth is the lightweight CollectObsidian structure: `AI/`, `Clippings/`, `Raw/`, `Resources/`, and `Templates/`.

If any repository document conflicts with this skill, follow this skill first.

## Required Context

Before editing any clipping, read:

1. `references/collect-obsidian-rules.md`
2. `AI/README.md`
3. `README.md`

## Safety Rules

- Run `git status --short` before reading or moving clippings.
- If there are uncommitted changes, report the summary and create a pre-processing snapshot commit only after the user explicitly confirms it.
- If the worktree is clean, explicitly say no pre-processing snapshot commit is needed.
- Do not create `Notes/`, `Areas/`, `Archives/`, or PARA directories unless the user explicitly requests them.
- Do not create subdirectories inside `Clippings/`.
- Do not delete original clipping files after processing; move them to `Raw/` as source archives.
- Do not read or reprocess files under `Raw/` unless the user explicitly asks to inspect an archived source.
- Do not fabricate source, author, publication date, or other metadata.
- Do not create the post-processing commit until the user confirms after reviewing the report and diff.

## Workflow

1. Scan `Clippings/*.md`, excluding `Clippings/README.md`.
2. Process every non-README Markdown file in `Clippings/`, not just new files or a single article.
3. For each clipping, read the full content once from `Clippings/`, determine the destination, create a cleaned resource note, move the original clipping to `Raw/`, and update indexes.
4. Prefer `Resources/` and existing or reasonable subdirectories such as `Resources/AI/` and `Resources/Tools/`.
5. Update `00-Home.md`.
6. If the destination directory has `README.md`, update its listing.
7. Finish with a processing report using the format in `references/collect-obsidian-rules.md`.

## Output Standards

- Write generated summaries, key points, and action items in Traditional Chinese.
- Keep formal resource notes concise; do not embed the full original article when the original clipping is archived in `Raw/`.
- Preserve source traceability with the original URL and a link to the archived raw clipping when useful.
- Use Obsidian wiki links where useful.
- Use namespace tags such as `type/clipping` and `status/processed`.
- Rename processed resource notes and archived raw clippings as `YYYY-MM-DD - 中文標題.md`.

## Common Mistakes

| Mistake | Correction |
|---|---|
| Processing only the newest clipping | Process all non-README Markdown files under `Clippings/`. |
| Committing after processing automatically | Stop after the report and wait for user confirmation. |
| Deleting the original clipping after creating a resource note | Move the original clipping to `Raw/` and link to it when useful. |
| Reprocessing archived originals | Scan `Clippings/` only; ignore `Raw/` unless the user explicitly asks for source inspection. |
