# CLAUDE.md — Volcatech 官網 Demo 專案指示

> 本檔由 Claude Code 自動讀取。接手本專案的任何 AI 助手與開發者都應遵守以下規則。

## 回覆語言

一律以繁體中文回覆;程式碼、指令、專有名詞與技術術語保留原文。

## 這個專案是什麼

沃凱科技(Volcatech)新官網的 demo 專案。**2026-07-31 內部評選已結束**,勝出組合為
**style-3-soc(SOC Console 深色色系)× 原版直落版型**,色系凍結;現階段工作是在勝出風格上
比對**兩種頂部選單變體**(正本:`docs/meeting_0731.md`):

- `style-3-soc/index.html` = **Nav A(單層)**:三個下拉,下拉內用 mono 小標(`li.grp`)分組。
- `style-3-soc/index-nav-b.html` = **Nav B(二層)**:分組升級為第二層 flyout(hover/focus-within 展開)。
- 產品頁(皆用 Nav A;選單擇一定稿後統一):`sentinelone.html`、`threatsonar.html`、`cybereyes.html`、
  `google-secops.html`(2026-08-03 依 `docs/product/` 內部素材新建);另有方案頁 `ess.html`
  (ESS=沃凱打包方案 WDR+EDR+7x24 SOC,非 19 項 SKU;**全頁零外部連結**,入口在 Services 下拉)。
- 選單分類已依會議決議由 Platform / Arsenal / Operations 改為
  **`Google Cloud` / `CyberSecurity` / `Services`**(`CyberSecurity` 駝峰是會議指定的刻意寫法,
  勿「順手修正」成 Cybersecurity;正文與板塊名仍用 Cybersecurity)。
  Google Cloud 下拉= GCP 產品樹六組 18 項(Compute / Storage / Analytics / Serverless / Databases / AI,
  產品資料正本:`docs/GCP_Introduce.md`);CyberSecurity =原 8 項(EDR / **SIEM & WDR** / Built in-house,
  SentinelOne·ThreatSonar·CyberEyes·Google SecOps 已連真頁;WDR 併記是因 CyberEyes 實為 WDR);
  Services =原 5 項＋頂部 ESS 方案入口。每個下拉第一行保留 mono 白話對照(`li.head`)。

評選期的 4 個色系風格(style-1/2/4)、4 個版型變體(layout-1〜4)與外部 AI 參考組
已全部**凍結封存於 `archive/`**(舊評選總覽= `archive/index.html`),一律不再修改;
根 `index.html` 已改為聚焦 style-3 與雙變體比對的 Demo hub。

- 目標受眾:歐洲企業的 IT / 資安決策者;語言英文為主(正式版另有繁中 /zh-tw/,架構須可擴充更多語系)
- 新官網將**改版取代**現有 volcatech.com
- 公司事實唯一可信來源:`docs/公司_104.md`(僅可用於服務範圍與願景,**不可**用來填統編/VAT/地址)
- 下一步:選單定稿後補齊其餘 15 個產品/服務頁(4 項已建,素材正本 `docs/product/`),再依 `docs/Volcatech_多風格_Build_Prompts.md`
  的「共用基底 + 勝出風格模組」產生正式 **Astro** 版(雙語 i18n、GDPR 隱私頁、sitemap/hreflang)
- **唯一事實來源(SSOT)**:`docs/Volcatech_多風格_Build_Prompts.md`(§A 19 項服務清單仍有效;
  §B style-3 模組的選單逐字定義為**評選期歷史**,選單分類以本檔上述 0731 決議為準)。
  `docs/官網建置計畫_Build_Prompt_v3.md` 已凍結為 **legacy**(僅供背景脈絡,勿照做)。

## 硬性規則(所有修改必須遵守)

1. **純靜態、單檔自足**:demo 頁為 HTML + inline CSS(+極少量原生 JS,僅限手機選單/下拉);
   禁止外部 CDN(含 Google Fonts,GDPR)、禁止前端框架、禁止建置步驟。
2. **相對路徑**:所有連結與資源用相對路徑(需相容 GitHub Pages 子路徑 `/repo名稱/`)。
3. **首屏鐵則**:首頁首屏必須有 H1 一句話 + 明列**三條業務板塊**
   (Cloud Infrastructure / Cybersecurity / Managed Services)各附入口連結。
   任何改版不得破壞「3 秒看懂賣什麼(雲端 + 資安 + 託管維運)」。
   - H1 定稿(不得改寫):
     `Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`
   - 副標定稿:`We design and run Google Cloud environments for European organisations, deploy and tune
     EDR and SIEM, and keep both under 24/7 monitoring. One team, one contract, one point of accountability.`
   - hero 文案(status 行 / H1 / 副標 / CTA)為**置中**呈現(0731 決議),下方 console 卡片維持靠左。
   - 首頁必備第 4 區 **Built by Volcatech**(自研 CE-BAS / AI-PTaaS / SecPurple):
     它是首頁區塊,**不是**第 4 條產品線,**不進頂層導覽**。
4. **不虛構公司事實**:統編、地址、認證(ISO 等)、客戶案例、合作等級一律 `[TODO: 說明]` 佔位,待確認才填。
   **全案只用 `[TODO: 說明]` 一種佔位語法**(不得用 `{{TODO}}`);建置參數用 `[VAR: 名稱]`。
5. **現行頁面只有 `style-3-soc/`**(design tokens 在各頁 `:root`);`archive/` 內所有頁面
   一律凍結不動——發現其中的問題只回報,不動手(理由見下方 archive 專節)。
6. **無障礙與品質**:WCAG 2.2 AA 對比、`:focus-visible`、`prefers-reduced-motion`、
   語意化 HTML、每頁唯一 `<h1>`、RWD(390 / 768 / 1024 / 1440px、無水平捲軸)。
7. **文案**:歐洲 B2B 直述語氣(做什麼、給誰、成果),禁「最先進/領導品牌」等 hype;
   日期用 `30 Jul 2026` 或 ISO 8601、24 小時制、電話 +886 國際格式、不放 LINE。
8. **原廠產品描述必須改寫**,不得複製原廠官網文案;外連原廠網站用 `target="_blank" rel="noopener"`。

## 現行風格 tokens 速查(style-3-soc)

| 項目 | 值 |
|---|---|
| bg / ink | #0E141F / #E9EEF5 |
| accent | #FFB224(+狀態綠 #3ECF8E 僅圓點) |
| 字體(正式版 @fontsource) | IBM Plex Sans + Plex Mono |
| 簽名元素 | mono 狀態列 + 狀態點(pulse 動畫,respect reduced-motion) |
| Nav 結構 | `Google Cloud ▾ / CyberSecurity ▾ / Services ▾`;每個下拉首行為 mono 白話對照;Nav A 單層 grp 分組 / Nav B 二層 flyout(`li.sub`,子代選擇器 `>`) |

額外禁止事項(評選期規則,仍適用):無 glow、無純黑、琥珀不得用於連結與小字、正文禁 ALL CAPS
(mono 微標籤如 `li.head`/`li.grp`/status 行不在此限)。
歷史四風格的 tokens 對照見 `archive/index.html` 或 `docs/Volcatech_多風格_Build_Prompts.md` §B。

## 兩變體一致性鐵則(選單比對有效性的前提)

比的是「選單層級」,不是內容。因此:

- `index.html` 與 `index-nav-b.html` **自 `<main>` 起逐字節相同**(含 footer 與 backlink 列);
  唯一允許差異= `<head>` 的 title 與選單相關 CSS、`<header>` 內的選單結構與自我參照連結。
- 兩檔的下拉**項目名稱與順序完全相同**,只有層級呈現不同(A: `li.grp` 小標;B: `li.sub` 二層)。
- 改任何共用內容(hero、卡片、Built、Why、Trust、footer)→ **兩檔一起改**,
  並跑 §驗證方式 的 `<main>` diff 檢查;動到 nav 項目或 footer 清單 → **全站 7 檔同步**
  (兩變體＋5 個子頁;子頁的錨點連結帶 `index.html` 前綴、同資料夾頁面用相對檔名)。

## 封存區:`archive/`(唯讀,平常不動它)

**是什麼**:0731 評選結束後封存的全部評選材料——`style-1-zurich/`、`style-2-nordic/`、
`style-4-continental/`、`layout-1〜4/` 四個版型變體、外部 AI 參考組
`Volcatech_Layout_Variants_GPT/`,與當時的評選總覽 `archive/index.html`(帶已歸檔橫幅)。

1. **一律不修改**:凍結的意義是保留評選當時的狀態供回顧;發現問題只回報。
   唯一例外:`archive/index.html` 的導流連結(指向根與 style-3 的部分)壞了可修。
2. **不 review**:§驗證方式 的檢查**不涵蓋 archive/**,不要為了「檢查完整」把它加進 glob。
3. **外部 AI 參考組**(`archive/Volcatech_Layout_Variants_GPT/`)延續原規則:唯讀、
   它自帶的 CLAUDE.md / README / HANDOVER 不適用於本專案(規則一律以根目錄本檔為準)、
   不套 tokens、不補連結。若要採用它的做法,是把做法**移植到現行 `style-3-soc/` 或未來 Astro 版**,
   不是就地改它;比對報告放 `docs/reports/`(帶日期)。
4. 線上網址:被封存的 demo 在 GitHub Pages 的路徑多一層 `/archive/`(舊連結會 404,
   由 `archive/index.html` 收容導流);`style-3-soc/` 路徑不變。

## 常見任務怎麼做

- **微調現行風格**:只改 `style-3-soc/` 內三個 html 的 tokens 與 CSS;
  共用內容三頁同步、兩變體跑 `<main>` diff(見一致性鐵則)。
- **調整選單**:項目與分類名以本檔 0731 決議為準;GCP 產品名以 `docs/GCP_Introduce.md`
  (2026-08-03 依官方查證)為準;三處(index / index-nav-b / sentinelone)同步。
  Nav B 的 flyout 顯示規則必須用**子代選擇器**(`.dd:hover>ul` 等),
  後代選擇器會讓巢狀層全開。
- **補產品頁**:複製 `style-3-soc/sentinelone.html` → 改 `<title>`、meta description、
  eyebrow 索引碼、內容區塊;產品清單(19 項,含代碼、slug 與原廠網址)見
  `docs/Volcatech_多風格_Build_Prompts.md` §A,素材見 `docs/product/`(內部,先讀產品簡介總覽.md)。
  **模板三坑**:`aria-current="page"` 搬到自己的 nav 項、語言切換 EN 的 href 改自己檔名、
  換成真連結的項刪 `title="Demo:…"`。完成後全站 7 檔的導覽列/頁尾對應項換真連結,功能卡保持偶數張。
- **選單定稿後**:勝出變體留為 `index.html`,另一變體移入 `archive/`(或依使用者指示刪除),
  並同步根 `index.html`、README、HANDOVER 與本檔。
- **產生正式 Astro 版**:不要改造本 demo;在新資料夾/新 repo 依
  `docs/Volcatech_多風格_Build_Prompts.md`(基底 + style-3 模組,選單分類以 0731 決議覆蓋)執行,
  完成後跑該檔【品質底線(驗收)】清單(**不是** v3 的 §9,那份已失效)。

## 檔案放置規約(維持根目錄乾淨)

**專案根 = 本檔所在目錄**(`/Users/shiro/Work/Volcatech_Web/`);CLAUDE.md、README.md 與 docs 內
所有相對路徑皆以此為基準。

| 要放什麼 | 放哪 |
|---|---|
| 規劃書、需求、prompt 集、會議記錄 | `docs/` |
| 一次性腳本、比對報告、體檢輸出 | 臨時 → scratchpad;要保留 → `docs/reports/`(檔名帶日期) |
| 現行風格的頁面與資產 | 只在 `style-3-soc/` 內 |
| 評選期封存材料(含外部 AI 參考組) | `archive/`,凍結不動 |
| 勝出風格的正式 Astro 版 | 新資料夾 `site/`,**不改動本 demo** |
| 制度檔(本檔、HANDOVER.md 等)修改前的備份 | `docs/backups/`,檔名加 `.bak-YYYYMMDD`(即全域維護協議所稱「專案備份目錄」的本專案對應) |

根目錄只允許:`index.html`、`README.md`、`CLAUDE.md`、`HANDOVER.md`、`.gitignore`、`.nojekyll`
與上表資料夾(`.vscode/`、`.github/` 除外)。**不要在根目錄新增散檔**;
`.DS_Store` 等系統檔已由 `.gitignore` 排除。

根目錄文件分工:`README.md` = 對外接手指南(本機預覽與 GitHub Pages 部署步驟的正本、專案結構圖);
`HANDOVER.md` = 進度與交接速查(規格正本仍在 `docs/`);
`.github/copilot-instructions.md` = 本檔硬性規則的濃縮副本(供 GitHub Copilot 使用者)。

**版控範圍**:demo 推到 public repo 供瀏覽,`docs/` 已列入 `.gitignore`
(內部建置計畫不對外),因此**頁面內不得連結 `docs/` 內的檔案**,否則線上會是死連結。
`.nojekyll` 用於關閉 GitHub Pages 的 Jekyll 處理,勿刪。

## 驗證方式(改完必做)

> **檢查範圍**:只含根 `index.html` 與 `style-3-soc/`。
> `archive/` 是凍結封存區,**不在檢查範圍內**——下列指令的 glob 刻意不涵蓋它,
> 不要為了湊「全站掃過」而把它加進去(理由見上方 archive 專節)。

```bash
python3 -m http.server 8000   # 開 http://localhost:8000 逐頁檢查(含 390px 寬)
```

- HTML 標籤配對可用 Python `html.parser` 快速檢查
- 確認頁面無外部資源請求(DevTools Network 只該有本機檔案):
  `grep -nE '<img |<script src|@import|<link ' style-3-soc/*.html` 應為空;
  `grep -noE 'https?://[^"]+' style-3-soc/*.html` 只該出現原廠 anchor 且同行有 `rel="noopener"`
  (全站唯一 JS 是各頁 navbtn 的行內 onclick 一行式;不得新增 `<script>` 標籤)
- 深色長文可讀性特別檢查;對比可用 DevTools 的 contrast checker
- Nav B 桌機檢查:hover 斜移進 flyout 不掉層、純鍵盤 Tab 全程可達、1024px flyout 不出視窗

### 一致性檢查(改過 style-3 任何頁面後必跑)

```bash
# 兩變體自 <main> 起逐字節相同 → 應無輸出
diff <(awk '/<main>/,0' style-3-soc/index.html) <(awk '/<main>/,0' style-3-soc/index-nav-b.html)
# H1 兩個首頁逐字相同 → 應輸出 2
grep -Fl 'from one turn-key partner.' style-3-soc/index*.html | wc -l
# section 順序兩檔必須完全一致(top→offer→built→why→trust→vendors→contact→legal)
for f in style-3-soc/index*.html; do echo -n "$f: "; \
  grep -o 'id="\(top\|offer\|built\|why\|trust\|vendors\|contact\|legal\)"' "$f" | tr '\n' ' '; echo; done
# CTA 一律 Contact us(sentence case);禁 Contact Us、禁 Request a proposal(那是 style-4 的刻意變因)
grep -oh 'Contact us\|Contact Us\|Request a proposal' style-3-soc/*.html | sort | uniq -c
# 死連結:每檔應只剩語言切換的 1 個
grep -c 'href="#"' style-3-soc/*.html
# 「繁中」每筆同行都要有 lang 屬性 → 應輸出 0
grep -h '繁中' style-3-soc/*.html | grep -vc 'lang="zh-Hant-TW"'
# 舊選單術語不得殘留 → 每檔應輸出 0
grep -c 'Arsenal\|>Platform<\|>Operations<' style-3-soc/*.html
# title 與 meta description 全站唯一 → 兩行皆應無輸出
grep -h '<title>' style-3-soc/*.html | sort | uniq -d
grep -h 'name="description"' style-3-soc/*.html | sort | uniq -d
# aria-current 每檔=3(1 個 markup + 2 個 CSS 選擇器);markup 在首頁=Home、子頁=自己的 nav 項
grep -c 'aria-current="page"' style-3-soc/*.html
# ess.html 方案頁零外部連結 → 應輸出 0
grep -c 'https\?://' style-3-soc/ess.html
# 5 個子頁 footer 與 sentinelone 逐字節相同 → 應輸出 4 行 OK
for f in threatsonar cybereyes google-secops ess; do \
  diff <(awk '/<footer/,/<\/footer>/' style-3-soc/sentinelone.html) \
       <(awk '/<footer/,/<\/footer>/' style-3-soc/$f.html) >/dev/null && echo "$f OK"; done
# 相對連結存在性(根 + style-3 + archive 入口)可用 python 一次掃(見 docs/reports/ 既往腳本或現寫)
```
