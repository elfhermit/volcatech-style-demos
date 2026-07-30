# CLAUDE.md — Volcatech 官網風格 Demo 專案指示

> 本檔由 Claude Code 自動讀取。接手本專案的任何 AI 助手與開發者都應遵守以下規則。

## 回覆語言

一律以繁體中文回覆;程式碼、指令、專有名詞與技術術語保留原文。

## 這個專案是什麼

沃凱科技(Volcatech)新官網的**風格評選 demo**:同一套網站骨架(內容、選單、資訊架構完全相同),
做成 4 個歐洲設計風格,供內部評選。每個風格 2 頁:`index.html`(首頁)+ `sentinelone.html`(產品頁範例)。

- 目標受眾:歐洲企業的 IT / 資安決策者;語言英文為主(正式版另有繁中 /zh-tw/)
- 新官網將**改版取代**現有 volcatech.com
- 勝出風格確定後,依 `docs/Volcatech_多風格_Build_Prompts.md` 的「共用基底 + 勝出風格模組」
  產生正式 **Astro** 版(雙語 i18n、11 個產品頁、GDPR 隱私頁、sitemap/hreflang)
- 完整規劃:`docs/官網建置計畫_Build_Prompt_v3.md`

## 硬性規則(所有修改必須遵守)

1. **純靜態、單檔自足**:demo 頁為 HTML + inline CSS(+極少量原生 JS,僅限手機選單/下拉);
   禁止外部 CDN(含 Google Fonts,GDPR)、禁止前端框架、禁止建置步驟。
2. **相對路徑**:所有連結與資源用相對路徑(需相容 GitHub Pages 子路徑 `/repo名稱/`)。
3. **首屏鐵則**:首頁首屏必須有 H1 一句話 + 明列三條產品線
   (Google Cloud services / Security products EDR·SIEM / Managed security)各附入口連結。
   任何改版不得破壞「3 秒看懂賣什麼」。
4. **不虛構公司事實**:統編、地址、認證(ISO 等)、客戶案例、合作等級一律 `[TODO]` 佔位,待確認才填。
5. **風格隔離**:每個 `style-*` 資料夾有自己的 design tokens(`:root` CSS variables),
   不可跨資料夾混用;調整某風格只改該資料夾。
6. **無障礙與品質**:WCAG 2.2 AA 對比、`:focus-visible`、`prefers-reduced-motion`、
   語意化 HTML、每頁唯一 `<h1>`、RWD(390 / 768 / 1024 / 1440px、無水平捲軸)。
7. **文案**:歐洲 B2B 直述語氣(做什麼、給誰、成果),禁「最先進/領導品牌」等 hype;
   日期用 `30 Jul 2026` 或 ISO 8601、24 小時制、電話 +886 國際格式、不放 LINE。
8. **原廠產品描述必須改寫**,不得複製原廠官網文案;外連原廠網站用 `target="_blank" rel="noopener"`。

## 風格 tokens 速查

| 風格 | bg / ink | accent | 字體(正式版 @fontsource) | 簽名元素 |
|---|---|---|---|---|
| style-1-zurich | #F7F7F5 / #1A1A1A | #1D4ED8 | Space Grotesk + Inter | 型錄索引碼 + 細網格 hero |
| style-2-nordic | #FBFAF7 / #1C2321 | #2E5A4E | Source Serif 4(僅 H1/H2)+ Inter | 目錄式 Hero |
| style-3-soc | #0E141F / #E9EEF5 | #FFB224(+狀態綠 #3ECF8E 僅圓點) | IBM Plex Sans + Plex Mono | mono 狀態列 + 狀態點 |
| style-4-continental | #FFFFFF / #14181D | #0F3D8A(+規範紅 #C8102E 僅細線) | Barlow + Inter | 規格書卡片 + 編號章節 |

各風格「額外禁止事項」見 `docs/Volcatech_多風格_Build_Prompts.md` §B 對應模組。

## 常見任務怎麼做

- **微調某風格**:只改該資料夾兩個 html 的 `:root` tokens 與相關 CSS;兩頁需同步。
- **為勝出風格補產品頁**:複製該風格 `sentinelone.html` → 改 `<title>`、meta description、
  eyebrow 索引碼、內容區塊;產品清單(11 項,含 slug 與原廠網址)見
  `docs/Volcatech_多風格_Build_Prompts.md` §A;完成後把該頁在導覽列/頁尾的 `href="#"` 換成實際連結。
- **新增混搭風格**:建 `style-5-hybrid/`,以指定風格為基底、只替換指定區塊;
  並在根目錄 `index.html` 總覽加卡片。
- **產生正式 Astro 版**:不要改造本 demo;在新資料夾/新 repo 依
  `docs/Volcatech_多風格_Build_Prompts.md`(基底 + 勝出模組)執行,
  完成後跑 `docs/官網建置計畫_Build_Prompt_v3.md` §9 驗收清單。

## 檔案放置規約(維持根目錄乾淨)

**專案根 = 本檔所在目錄**(`/Users/shiro/Work/Volcatech_Web/`);CLAUDE.md、README.md 與 docs 內
所有相對路徑皆以此為基準。

| 要放什麼 | 放哪 |
|---|---|
| 規劃書、需求、prompt 集 | `docs/` |
| 一次性腳本、比對報告、體檢輸出 | 臨時 → scratchpad;要保留 → `docs/reports/`(檔名帶日期) |
| 某風格的頁面與資產 | 只在對應 `style-*/` 內 |
| 勝出風格的正式 Astro 版 | 新資料夾 `site/`,**不改動本 demo** |

根目錄只允許:`index.html`、`README.md`、`CLAUDE.md`、`.gitignore`、`.nojekyll` 與上表資料夾
(`.vscode/`、`.github/` 除外)。**不要在根目錄新增散檔**;`.DS_Store` 等系統檔已由 `.gitignore` 排除。

**版控範圍**:demo 推到 public repo 供評選瀏覽,`docs/` 已列入 `.gitignore`
(內部建置計畫不對外),因此**頁面內不得連結 `docs/` 內的檔案**,否則線上會是死連結。
`.nojekyll` 用於關閉 GitHub Pages 的 Jekyll 處理,勿刪。

## 驗證方式(改完必做)

```bash
python3 -m http.server 8000   # 開 http://localhost:8000 逐頁檢查(含 390px 寬)
```

- HTML 標籤配對可用 Python `html.parser` 快速檢查
- 確認頁面無外部資源請求(DevTools Network 只該有本機檔案)
- 深色 style-3 特別檢查長文可讀性;對比可用 DevTools 的 contrast checker
