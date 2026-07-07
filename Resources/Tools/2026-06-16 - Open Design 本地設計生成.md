---
title: "Open Design 本地設計生成"
date: "2026-06-16"
source: "https://yujustcoding.com/step-by-step/open-design-claude-alternative.html"
author: "[[Yui]]"
published: "2026-05-05"
category: "Resources/Tools"
tags:
  - type/clipping
  - status/processed
  - type/resource
  - topic/design-tool
  - topic/local-ai
summary: "Open Design 是可本地執行、支援多種 AI CLI 的設計生成工具。"
key_points:
  - "可替代部分 Claude Design 工作流"
  - "設計資料保存在本機 SQLite"
  - "支援 Codex、Claude Code、Cursor 等 CLI"
  - "提供 Skills 與 Design Systems"
  - "可透過 MCP 接入既有工具鏈"
actionable: "若需要本地設計原型工具，可先測試 Open Design 與 Codex 的 CLI 整合。"
---

# 📎 Open Design 本地設計生成

## 摘要

> Open Design 是一個免費開源的本地設計生成工具，目標是降低 Claude Design 的訂閱、雲端與工具鎖定限制。它可搭配多種 AI CLI 生成網頁、行動裝置、簡報、圖片與影片原型，並能透過 MCP 接入既有開發流程。

## 重點

- Claude Design 的限制在於工具鎖定、雲端依賴與 Claude Max 訂閱成本。
- Open Design 將設計生成放回本地執行，設計資料存在本機 SQLite。
- 工具可自動偵測 Claude Code、Codex、Cursor Agent、Gemini CLI 等多種 AI CLI。
- 啟動後可選 Skill 與 Design System，生成後在本地沙箱預覽並匯出。
- Open Design 提供 stdio MCP server，可讓外部 agent 查詢本地專案的設計資源。

## 可行動事項

- [ ] 在測試資料夾中安裝 Open Design，確認本機 Node.js、pnpm 與 Codex CLI 整合是否符合自己的工作流。

## 原文整理

原文將 Open Design 定位為 Claude Design 的開源替代方案。Claude Design 可從文字描述生成 UI 原型與網頁布局，但需要 Claude Desktop 與 Claude Max 訂閱，且運算在 Anthropic 雲端執行。

Open Design 的不同點是：它由 nexu-io 維護，將設計生成工具放在本機執行，不需訂閱 Claude Max，也不綁定特定 AI 工具。原文提到它支援 Cursor Agent、Gemini CLI、Codex 等多種 AI CLI。

### Claude Design 的限制

原文歸納 Claude Design 的三個限制：

- 工具鎖定：只能在 Claude 對話介面中使用，不容易接進 Cursor、Gemini CLI 或其他流程。
- 雲端依賴：所有設計任務需送到 Anthropic 伺服器，對客戶專案或公司內部設計可能有保密顧慮。
- 訂閱費用：若只是偶爾使用設計生成，Claude Max 的月費成本效益不一定合適。

Open Design 試圖同時移除這三個問題。

### Open Design 是什麼

Open Design 是開源的本地設計生成工具，專案位於 GitHub，由 nexu-io 維護。啟動後會載入多個 Skills 與 Design Systems，可生成的輸出包括網頁、桌面、行動裝置 HTML 原型、簡報、圖片、影片，以及 HyperFrames 互動式設計框架。

所有產出可在本地沙箱環境預覽，確認後再匯出。設計資料保存在本機 SQLite 資料庫，不會送到外部服務。

### 支援的 AI CLI

Open Design 啟動時會自動偵測環境中已安裝的 AI CLI。原文列出的支援清單包括：

- Claude Code
- Codex
- Cursor Agent
- Gemini CLI
- OpenCode
- Qwen CLI
- GitHub Copilot
- Hermes
- Kimi CLI

如果有 Anthropic API key，也可在介面中貼入並走 BYOK 路徑。

### 安裝步驟

原文列出環境需求為 Node.js v24 以上與 pnpm 10.33.x，可先確認版本：

```bash
node -v
pnpm -v
```

Clone 專案並安裝依賴：

```bash
git clone https://github.com/nexu-io/open-design.git
cd open-design
corepack enable
pnpm install
```

啟動 Web 介面：

```bash
pnpm tools-dev run web
```

第一次啟動時，系統會建立 `.od/` 資料夾，存放 SQLite 專案資料庫與歷史產出紀錄。

### 基本操作流程

啟動後，使用者主要選擇 AI CLI 與 Design System。預設使用 `web-prototype` skill 和 `Neutral Modern` 設計系統，適合快速上手。

操作方式是直接描述想要的設計，選擇對應 Skill，讓 AI agent 生成產出，右側即時預覽，確認後再匯出。Design Systems 會套用對應色彩與排版規則。

### MCP 整合

Open Design 附帶 stdio MCP server，可接進 Claude Code、Codex、Cursor 或任何支援 MCP 的客戶端。接上後，外部 agent 可以查詢本地 Open Design 專案中的設計資源，包括 Design Token、CSS 變數、JSX 元件與 HTML 入口檔。回傳的是目前檔案狀態，而不是舊匯出版本。

### 常見問題整理

原文說明，不一定需要 Anthropic API key；若已安裝其他支援的 AI CLI，Open Design 可以直接使用。匯出的 HTML 原型可作為前端開發起點，PPTX 也可在 PowerPoint 或 Keynote 中繼續編輯。

離線能力取決於使用情境：本地設計系統選擇與預覽可離線，AI 生成則取決於所選 CLI 本身是否可離線。輸出品質也主要取決於使用的 AI CLI 與 Design System。

### 原文結論

Claude Design 將設計生成綁在訂閱制與雲端服務上，Open Design 則把類似能力搬回本地，讓使用者自行選擇 AI 工具、控制資料位置，也避免為偶爾使用的功能支付月費。若在意工具自由度或資料保密，可先試用 Open Design。

## 相關筆記

- [[Resources/AI/2026-07-03 - Codex 個人站設計流程]]
- [[Resources/AI/2026-05-27 - Taste Skill AI 前端設計技能]]
- [[Resources/Tools/2026-05-15 - html-anything Agent HTML 生成工具]]

## 來源

- 原文：[Claude Design 做不到的事，Open Design 開源全做到了](https://yujustcoding.com/step-by-step/open-design-claude-alternative.html)
- 作者：[[Yui]]
