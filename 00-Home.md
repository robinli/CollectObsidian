---
title: 知識庫首頁
date: 2026-05-06
tags:
  - MOC
  - index
---

# 知識庫首頁

> 目前只保留 AI、Clippings、Resources、Templates 四個工作區。

## 收集

- [[Clippings/README|Clippings — 原始收集區]]

```dataview
TABLE source, summary, date
FROM "Clippings"
WHERE file.name != "README"
SORT date DESC
```

## 最近整理

- [[Resources/AI/2026-07-10 - LLM 知識庫整理提示詞]]
- [[Resources/AI/2026-07-08 - AI 知識工作流十個原則]]

- [[Resources/AI/2026-07-07 - Obsidian Codex 個人知識庫]]
- [[Resources/AI/2026-07-07 - AI 記憶系統三步驟]]
- [[Resources/AI/2026-07-03 - Codex 個人站設計流程]]
- [[Resources/Tools/2026-06-16 - Open Design 本地設計生成]]
- [[Resources/AI/2026-05-27 - Codex 入門完整教學]]
- [[Resources/AI/2026-05-27 - Taste Skill AI 前端設計技能]]
- [[Resources/Tools/2026-05-27 - CodeGraph 節省 AI 編碼 Token]]
- [[Resources/AI/2026-05-27 - Codex 一手包辦辦公流程自動化]]
- [[Resources/Tools/2026-05-23 - Docker 從入門到實踐]]
- [[Resources/AI/2026-05-22 - Anthropic 多晶片算力佈局]]
- [[Resources/Tools/2026-05-22 - Google AI Studio 網頁讀取實測]]
- [[Resources/AI/2026-05-21 - Markdown 給 AI HTML 給人看]]
- [[Resources/AI/2026-05-20 - Microsoft AI Agents 入門 12 課]]
- [[Resources/AI/2026-05-20 - Microsoft Agent Framework 與 Skill 解耦]]
- [[Resources/Tools/2026-05-20 - LINE 語音轉文字 Webhook 實作]]
- [[Resources/Tools/2026-05-15 - html-anything Agent HTML 生成工具]]

## 整理後參考資源

- [[Resources/README|Resources — AI 整理後參考資源]]

```dataview
TABLE summary, tags, file.mtime AS "最後更新"
FROM "Resources"
SORT file.mtime DESC
LIMIT 20
```

## AI 說明

- [[AI/README|AI — 給 AI 讀的整理規則]]

## 樣板

- [[Templates/README|Templates — 必要樣板]]

## 常用標籤

| 標籤 | 說明 |
|------|------|
| `#status/draft` | 尚未整理 |
| `#status/review` | AI 已整理，待人工確認 |
| `#status/done` | 已確認可作為參考 |
| `#type/clipping` | 原始收集 |
| `#type/resource` | 整理後參考資源 |
