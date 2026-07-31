# Copilot 專案指示 — Volcatech 官網風格 Demos

一律以繁體中文回覆;程式碼與技術術語保留原文。完整規則見根目錄 `CLAUDE.md`,重點如下:

- 本專案為靜態評選 demo:第一輪 4 個歐洲設計風格 `style-*/`(每風格 `index.html` + `sentinelone.html`),
  第二輪 4 個版型變體 `layout-*/`(每變體 5 頁,另含 services / about / contact);
  勝出後依 `docs/Volcatech_多風格_Build_Prompts.md`(**唯一事實來源**)產生正式 Astro 版。
  `docs/官網建置計畫_Build_Prompt_v3.md` 已凍結為 legacy,其規格一律不採信。
- **`Volcatech_Layout_Variants_GPT/` 是外部 AI 參考組:唯讀,不要修改、不要 review、不納入任何檢查**。
  它自帶的 `CLAUDE.md` / `README.md` / `HANDOVER.md` 只描述它自己,**不適用本專案**;
  規則衝突時一律以根目錄 `CLAUDE.md` 為準。它的子資料夾與本專案 `layout-*/` 同名但內容獨立,
  編輯前先確認路徑前綴。要採用它的做法時,是移植到本專案的 `layout-*/`,不就地改它。
- 純靜態、單檔自足:HTML + inline CSS,禁止外部 CDN(含 Google Fonts)、禁止框架與建置步驟。
- 全站相對路徑(GitHub Pages 子路徑相容)。
- 首頁首屏必須保留:H1 + 明列**三條業務板塊**
  (Cloud Infrastructure / Cybersecurity / Managed Services)各附入口。
  H1 定稿(四風格逐字相同,不得改寫):
  `Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`
- 首頁必備 **Built by Volcatech** 區塊(自研 CE-BAS / AI-PTaaS / SecPurple);
  它不是第 4 條產品線,**不進頂層導覽**。
- **四風格一致性鐵則**:H1、副標、三線區、Built by Volcatech、Why、Trust、CTA band、
  footer legal 逐字相同,section 順序與 `id` 相同;差異只允許在選單組織方式與視覺層。
  改共用文案 → 四風格一起改。
- 公司事實(統編、地址、認證、案例)一律 `[TODO: 說明]` 佔位,不得虛構;
  **全案只用這一種佔位語法**(不得用 `{{TODO}}`)。公司事實來源為 `docs/公司_104.md`,
  但該檔只可用於服務範圍與願景,不可用來填統編/VAT/地址。
- 每個 `style-*` 資料夾的 design tokens 獨立,不可跨風格混用;同風格兩頁需同步修改。
- WCAG 2.2 AA、`:focus-visible`、`prefers-reduced-motion`、RWD(390/768/1024/1440)、每頁唯一 h1;
  非英文片段(如「繁中」、中文公司名)必須帶 `lang` 屬性。
- 文案為歐洲 B2B 直述語氣,禁 hype 形容詞(leading / best-in-class / cutting-edge)與
  絕對化承諾(every / all / 100%);禁正文 ALL CAPS;原廠產品描述必須改寫,不得複製。
