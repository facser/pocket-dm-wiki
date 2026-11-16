# AGENTS.md — 《Pocket DM》DND 5e 跑團與規則圖鑑知識庫開發規範

## 1. 專案目的 (Project Purpose)
本專案為《Pocket DM》DND 5e 智慧跑團系統的靜態知識庫與劇本圖鑑網站（托管於 GitHub Pages）。
目標是將《DND 5e 玩家手冊》的種族、職業、檢定規則以及經典跑團模組（如《迪利安之墓》）整理為結構化、可快速檢索且具奇幻桌面角色扮演（TRPG）沉浸感的網頁。任何 AI Agent 在協助新增或修改本專案內容時，必須嚴格遵守本文件之規範。

## 2. 整體視覺與技術風格 (Design & Tech Stack)
- **技術框架**：純靜態 HTML5 + Tailwind CSS (透過 CDN 引入)，不依賴複雜打包工具，確保 GitHub Pages 可直接渲染。
- **色彩規範 (Dark Fantasy Tavern Theme)**：
  - 背景主色：深邃地城黑 (`bg-slate-950`) 與羊皮紙深灰 (`bg-slate-900`)。
  - 強調色：傳奇金 (`text-amber-400`, `border-amber-500/30`) 與奧術紅 (`bg-rose-900/40`)。
  - 文字顏色：主文採用柔和米白 (`text-slate-200`)，次要資訊採用 (`text-slate-400`)。
- **排版與字體**：標題具備奇幻古卷質感（加粗、字距微調 `tracking-wide`），所有規則數值（如 `DC 15`、`1d20 + 3`、`HP`、`AC`）必須使用等寬字體標籤 (`font-mono`) 與徽章樣式標示。
- **語系規範**：全面使用**台灣習慣的繁體中文**（例如：使用「遊蕩者」而非「盜賊」、使用「屬性調整值」而非「修正值」），專有名詞可括號附上英文原文（如：`敏捷（Dexterity）`）。

## 3. 檔案命名與目錄結構 (File Naming & Directory Structure)
所有檔案必須遵循全小寫連字號（`kebab-case`）命名規則：
- `index.html`：知識庫首頁，包含分類導覽列、即時關鍵字篩選器與所有圖鑑的入口卡片（Card Grid）。
- `pages/race-[name].html`：種族介紹頁（例：`pages/race-elf.html`）。
- `pages/class-[name].html`：職業介紹頁（例：`pages/class-rogue.html`）。
- `pages/monster-[name].html`：怪物屬性卡頁面（例：`pages/monster-goblin.html`）。
- `pages/adventure-[name].html`：跑團劇本與遭遇戰指南（例：`pages/adventure-delian-tomb.html`）。

## 4. 頁面標準結構 (Standard Page Layout)
每一個新增的圖鑑內容或子頁面必須包含以下四個標準區塊：
1. **頂部導覽列 (Header Bar)**：包含返回首頁連結、分類麵包屑（Breadcrumb）與「🎲 快速檢定試算器」按鈕。
2. **核心屬性摘要卡 (Stat Block / Summary Header)**：
   - 顯示條目名稱、英文原名、分類標籤（種族 / 職業 / 怪物 / 劇本）。
   - 顯示關鍵數值徽章（例如：生命骰 `1d8`、主要屬性 `敏捷`、豁免熟練 `敏捷 & 智力` 或怪物 `AC` / `HP`）。
3. **規則與背景詳解區 (Lore & Mechanics Section)**：
   - 採用雙欄或分段卡片排版，明確區分「📖 背景故事 (Lore)」與「⚙️ 規則特質 (Mechanics)」。
4. **DM 跑團檢定建議框 (DM Check Callout)**：
   - 每個頁面底部必須包含一個琥珀色邊框的提示框，列出該條目常見的 **Tool Use 檢定情境與建議 DC**（例如：「使用盜賊工具撬開地精寶箱：`敏捷（巧手）DC 13`」）。

## 5. AI 新增或修改內容時的自動化工作流 (AI Workflow Rules)
當使用者要求 AI「新增一個條目（例如：新增矮人種族頁、新增哥布林怪物卡）」時，AI 必須依序執行以下步驟：
1. **檢查分類與命名**：確認條目類型，決定正確的檔名（如 `pages/race-dwarf.html`）與分類標籤（`data-category="race"`）。
2. **套用標準模板生成內容**：複製現有頁面的 Tailwind CSS 骨架，填入繁體中文規則、數值徽章與「DM 跑團檢定建議框」。
3. **同步更新首頁索引 (`index.html`)**：
   - 在 `index.html` 的 `#wiki-grid` 區塊中，新增一張對應的預覽卡片（需包含正確的 `data-category` 屬性以支援首頁按鈕篩選，以及關鍵字文字以支援即時搜尋）。
4. **禁止事項**：
   - 禁止捏造非 DND 5e SRD 官方規則的數值（若為自創房規，必須加上 `[自創規則 Homebrew]` 標籤）。
   - 禁止破壞現有的響應式網格（`grid-cols-1 md:grid-cols-2 lg:grid-cols-3`）與深色主題配色。