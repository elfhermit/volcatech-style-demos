# Copilot 專案指示 — Volcatech 官網風格 Demos

一律以繁體中文回覆;程式碼與技術術語保留原文。完整規則見根目錄 `CLAUDE.md`,重點如下:

- 本專案為 4 個歐洲設計風格的靜態 demo(每風格 `index.html` + `sentinelone.html`),
  用於評選;勝出後依 `docs/Volcatech_多風格_Build_Prompts.md` 產生正式 Astro 版。
- 純靜態、單檔自足:HTML + inline CSS,禁止外部 CDN(含 Google Fonts)、禁止框架與建置步驟。
- 全站相對路徑(GitHub Pages 子路徑相容)。
- 首頁首屏必須保留:H1 + 明列三條產品線(Cloud / Security products / Managed security)各附入口。
- 公司事實(統編、地址、認證、案例)一律 `[TODO]` 佔位,不得虛構。
- 每個 `style-*` 資料夾的 design tokens 獨立,不可跨風格混用;同風格兩頁需同步修改。
- WCAG 2.2 AA、`:focus-visible`、`prefers-reduced-motion`、RWD(390/768/1024/1440)、每頁唯一 h1。
- 文案為歐洲 B2B 直述語氣,禁 hype 形容詞;原廠產品描述必須改寫,不得複製。
