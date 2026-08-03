# Copilot 專案指示 — Volcatech 官網 Demo(勝出風格 style-3-soc)

一律以繁體中文回覆;程式碼與技術術語保留原文。完整規則見根目錄 `CLAUDE.md`,重點如下:

- 本專案為靜態官網 demo。**2026-07-31 內部評選已結束**:勝出組合 = Style 3(SOC Console
  深色色系)× 原版直落版型,色系凍結。現行維護對象只有 `style-3-soc/` 三頁:
  `index.html`(Nav A,單層下拉)、`index-nav-b.html`(Nav B,二層 flyout)、
  `sentinelone.html`(用 Nav A);根 `index.html` 是 Demo hub。
  正式版依 `docs/Volcatech_多風格_Build_Prompts.md`(**唯一事實來源**)產生 Astro 版;
  但該檔 §B 的 style-3 選單定義(Platform / Arsenal / Operations)是評選期歷史,
  現行選單以 `style-3-soc/` 頁面為準。`docs/官網建置計畫_Build_Prompt_v3.md` 已凍結為
  legacy,其規格一律不採信。
- **`archive/` 是已凍結的評選歷史(落選風格、版型變體、舊總覽):一律不修改、不 review、
  不納入任何檢查**。其中 `archive/Volcatech_Layout_Variants_GPT/` 是外部 AI 參考組,唯讀;
  它自帶的 `CLAUDE.md` / `README.md` / `HANDOVER.md` 只描述它自己,**不適用本專案**,
  規則衝突時一律以根目錄 `CLAUDE.md` 為準。
- **兩變體一致性鐵則**:`style-3-soc/index.html` 與 `index-nav-b.html` 自 `<main>` 起
  必須**逐字節相同**;改 `<main>` 之後的內容,兩檔必須同步並用 diff 驗證。
- 頂部選單分類為 `Google Cloud / CyberSecurity / Services`;`CyberSecurity` 駝峰是
  0731 會議指定的**刻意寫法**,不要「修正」成 Cybersecurity(僅限選單分類名,
  H1 等內文仍為定稿原文)。每個下拉第一行是 mono 白話對照。
- 純靜態、單檔自足:HTML + inline CSS,禁止外部 CDN(含 Google Fonts)、禁止框架與建置步驟。
- 全站相對路徑(GitHub Pages 子路徑相容)。
- 首頁首屏必須保留:H1 + 明列**三條業務板塊**
  (Cloud Infrastructure / Cybersecurity / Managed Services)各附入口。
  H1 定稿(不得改寫):
  `Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`
- 首頁必備 **Built by Volcatech** 區塊(自研 CE-BAS / AI-PTaaS / SecPurple);
  它不是第 4 條產品線,**不進頂層導覽**。
- 公司事實(統編、地址、認證、案例)一律 `[TODO: 說明]` 佔位,不得虛構;
  **全案只用這一種佔位語法**(不得用 `{{TODO}}`)。公司事實來源為 `docs/公司_104.md`,
  但該檔只可用於服務範圍與願景,不可用來填統編/VAT/地址。
- `style-3-soc/` 的 design tokens(`:root` CSS variables)獨立,不可從 `archive/` 舊風格
  混入;三頁的 tokens 與共用區塊需同步修改。
- WCAG 2.2 AA、`:focus-visible`、`prefers-reduced-motion`、RWD(390/768/1024/1440)、每頁唯一 h1;
  非英文片段(如「繁中」、中文公司名)必須帶 `lang` 屬性。
- 文案為歐洲 B2B 直述語氣,禁 hype 形容詞(leading / best-in-class / cutting-edge)與
  絕對化承諾(every / all / 100%);禁正文 ALL CAPS;原廠產品描述必須改寫,不得複製。
