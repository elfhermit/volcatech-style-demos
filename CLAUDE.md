# CLAUDE.md — Volcatech 官網 Demo 專案指示

> 本檔由 Claude Code 自動讀取。接手本專案的任何 AI 助手與開發者都應遵守以下規則。

## 回覆語言

一律以繁體中文回覆;程式碼、指令、專有名詞與技術術語保留原文。

## 這個專案是什麼

沃凱科技(Volcatech)新官網的 demo 專案。**2026-07-31 內部評選已結束**,勝出組合為
**style-3-soc(SOC Console 深色色系)× 原版直落版型**,色系凍結。
現階段有**兩個並行的比對軸**(選單正本:`docs/meeting_0731.md`;版面正本:本檔下方「版面變體」節):

**軸一:頂部選單變體(Nav A vs Nav B)**

- `style-3-soc/index.html` = **Nav A(單層)**:三個下拉,下拉內用 mono 小標(`li.grp`)分組。
- `style-3-soc/index-nav-b.html` = **Nav B(二層)**:分組升級為第二層 flyout(hover/focus-within 展開)。

**軸二:首頁版面變體(2026-08-04 新增,共 8 個首頁檔 = 4 方案 × Nav A/B)**

| 方案 | Nav A 檔名 | 押注 / hero 之後第一眼 |
|---|---|---|
| 現行(對照組) | `index.html` | 維持現狀:Built → Why → Trust → Vendors(六個純文字) |
| V1 信任前置 | `index-v1-proof.html` | **How we work** 三步驟 → Trust 四項(資料主權/存取控制) → Partners 六張能力卡 |
| V2 型錄前置 | `index-v2-catalogue.html` | **Service catalogue** 21 列表格(代碼｜名稱｜一句話｜Powered by) |
| V3 參考架構 | `index-v3-flow.html` | **Reference architecture** 四層圖(Web→端點→偵測→維運)＋Google Cloud 底座 |

Nav B 版一律是 `<Nav A 檔名>-nav-b.html`,由腳本從 Nav A 版換 header 產生,**不得手改**。
三個變體要解的是盤點出的三個結構性病灶:①「產品有哪些」動線斷在頁尾錨點;
②「合作夥伴」只有六個純文字品牌名、無語境;③「公司做什麼」缺交付流程與可驗證性。
變體共用的新區塊代號:`#how`(交付三步)、`#partners`(夥伴)、`#catalogue`(服務索引/型錄)、
`#stack`(V3 架構圖)。核心句 `We operate what we sell, and we build what we cannot buy.`
是三個變體共用的凍結文案(**對照組刻意不含**,故它在 8 個首頁中只命中 6 次)。
- 資安產品頁(皆用 Nav A;選單擇一定稿後統一):`sentinelone.html`、`threatsonar.html`、`cybereyes.html`、
  `google-secops.html`(2026-08-03 依 `docs/product/` 內部素材新建);另有方案頁 `ess.html`
  (ESS=沃凱打包方案 WDR+EDR+7x24 SOC,非 19 項 SKU;**全頁零外部連結**,入口在 Services 下拉)。
- **Cloud 線 8 頁**(2026-08-04 新建,內容正本= `docs/Cloud線_內容規劃_20260804.md`):
  `cloud.html`(總覽,CI)＋六個 GCP 分類頁 `cloud-compute` / `cloud-storage` / `cloud-analytics` /
  `cloud-serverless` / `cloud-databases` / `cloud-ai`(CI-01〜CI-06)＋
  `cloud-services.html`(CI-07,Cloud Armor＋沃凱雲端服務 3 項)。
  **分類頁骨架**比資安產品頁多一區「產品名冊」(`loglist`,每列帶 `id` 當深連結落點),
  `cards2` 固定 4 張改放「沃凱在這層交付什麼」——因為多數分類只有 3 個產品而 `cards2` 須偶數。
  **代碼分層**:`CI-*` 是頁面層(現行);`C-*`/`E-*`/`S-*`/`X-*` 是 SSOT §A 的 SKU 層,
  已於 2026-08-04 定案為 **pre-0731 歷史體系**,不對齊、不上站。
- 選單分類已依會議決議由 Platform / Arsenal / Operations 改為
  **`Google Cloud` / `CyberSecurity` / `Services`**(`CyberSecurity` 駝峰是會議指定的刻意寫法,
  勿「順手修正」成 Cybersecurity;正文與板塊名仍用 Cybersecurity)。
  Google Cloud 下拉= **六組 18 項**(Compute / Storage / Analytics / Serverless / Databases / AI),
  頂部另有 Overview 入口 → `cloud.html`;
  ⚠️ 2026-08-05 使用者指示**從選單移除** `Edge security`(Cloud Armor)與
  `Volcatech cloud services`(3 項)兩組——**只動選單**:頁尾的「Cloud services & Cloud Armor」、
  `cloud.html` 內的相關區塊與 `cloud-services.html` 頁面本身一律保留不動
  (腳本:`docs/reports/remove_gcp_groups_20260805.py`);
  **18 項全部是深連結**(`分類頁#產品錨點`),產品資料正本:`docs/GCP_Introduce.md`
  (2026-08-04 補入第 7 節 Cloud Armor);CyberSecurity =原 8 項(EDR / **SIEM & WDR** / Built in-house,
  SentinelOne·ThreatSonar·CyberEyes·Google SecOps 已連真頁;WDR 併記是因 CyberEyes 實為 WDR);
  Services =原 5 項＋頂部 ESS 方案入口。每個下拉第一行保留 mono 白話對照(`li.head`)。
  **Nav A 的 `.dd ul` 必須帶 `max-height`＋`overflow-y:auto`**(26 列在矮視窗會溢出);
  **Nav B 反之絕不可加 overflow**——會變成 clip container 裁掉二層 flyout,
  且它第一層只有 10 列不會溢出(理由已寫在 `index-nav-b.html` 的 CSS 註解)。

評選期的 4 個色系風格(style-1/2/4)、4 個版型變體(layout-1〜4)與外部 AI 參考組
已全部**凍結封存於 `archive/`**(舊評選總覽= `archive/index.html`),一律不再修改;
根 `index.html` 已改為 Demo hub:首屏是**四個版面方案的橫向比較**(現行/V1/V2/V3,每張卡寫明押注
與 section 序列,各附 Nav A/B 兩個入口),下方依序為兩個新總覽頁、style-3 全部內容頁、歷史存檔入口。
八個首頁檔底部另有 backlink 切換列(`Layout: Current · V1 · V2 · V3 · Nav: A · B`),
比較時不必回 hub。

- 目標受眾:歐洲企業的 IT / 資安決策者;語言英文為主(正式版另有繁中 /zh-tw/,架構須可擴充更多語系)
- 新官網將**改版取代**現有 volcatech.com
- 公司事實唯一可信來源:`docs/公司_104.md`(僅可用於服務範圍與願景,**不可**用來填統編/VAT/地址)。
  ⚠️ 2026-08-04 使用者指示**本次先不參考它**——Cloud 線的沃凱自有服務描述因此一律 `[TODO]`,
  待新素材;各頁 `cards2` 的交付卡是不含獨有宣稱的通用交付項,取得素材後須校正。
- 下一步:①`cloud-services.html` 的沃凱服務 3 段內文待素材;②補齊 Services 線其餘服務頁;
  ③選單擇一定稿後,另一變體移入 `archive/`;④再依 `docs/Volcatech_多風格_Build_Prompts.md`
  的「共用基底 + 勝出風格模組」產生正式 **Astro** 版(雙語 i18n、GDPR 隱私頁、sitemap/hreflang)
- **唯一事實來源(SSOT)**:`docs/Volcatech_多風格_Build_Prompts.md`(§A 19 項服務清單已於 2026-08-04
  定案為 **pre-0731 歷史體系**——保留封存、不改內容、新架構不對齊它;
  §B style-3 模組的選單逐字定義同為**評選期歷史**,選單分類以本檔上述 0731 決議為準)。
  Cloud 線的內容正本是 `docs/Cloud線_內容規劃_20260804.md`,不是 SSOT §A。
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

## 一致性鐵則:雙軸(兩條比對軸都成立的前提)

2026-08-04 起有 8 個首頁檔(4 個版面方案 × Nav A/B)。舊的單一鐵則
(「兩變體自 `<main>` 起逐字節相同」)已不適用於跨版面比對,改為雙軸:

### 軸 1|同一版面的 Nav A ↔ Nav B:自 `<main>` 起逐字節相同

比的是「選單層級」,不是內容。因此:

- 每一組 A/B **自 `<main>` 起逐字節相同**(含 footer 與 backlink 列);唯一允許差異=
  `<head>` 的 title/description 與選單相關 CSS、`<header>` 內的選單結構與自我參照連結。
- 兩檔的下拉**項目名稱與順序完全相同**,只有層級呈現不同(A: `li.grp` 小標;B: `li.sub` 二層)。
- ⚠ 坑:Nav B 母版的**頁尾 logo** 指向 `index.html` 而非自己,產生 Nav B 版時必須一併改成
  該變體的 Nav A 檔名,否則軸 1 diff 會紅在 `<footer>` 裡。
- **Nav B 版一律用腳本從 Nav A 版產生**(只換 `<header>`、title/description、自我參照連結),
  不得手改。共 4 組 diff 必須全部無輸出。

### 軸 2|跨版面方案:共用文案逐字凍結

不要求結構相同(結構就是變因),但共用文案必須逐字一致,否則會變成比文案而不是比版面
(踩過的坑:全域教訓簿 2026-07-30)。**凍結清單**:

| 句子 | 應命中的首頁檔數 |
|---|---|
| `Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`(H1) | 8 |
| `…deploy and tune EDR and SIEM… one point of accountability.`(副標) | 8 |
| `One partner accountable for the whole stack.`(Why H2) | 8 |
| `Tell us about your environment — we will map the path to cloud, security and operations.`(CTA) | 8 |
| `Cloud, security and managed operations for European organisations.`(footer 品牌句) | 8 |
| `We operate what we sell, and we build what we cannot buy.`(核心句) | **6**(僅三變體) |

最後一句刻意只在三個變體出現——`index.html` / `index-nav-b.html` 是**未經內容改動的對照組**,
代表「今天線上的樣子」,不得為了湊一致而修改它。

### 共同規則

- 四個方案的 **hero 區塊(`#top` 含 `#offer` 三張卡)完全相同**,差異一律從第二區塊開始。
- 改任何共用內容(hero、Built、Why、Trust、footer)→ **8 個首頁一起改**(改共用區塊後重跑產生腳本)。
- 動到 nav 項目或 footer 清單 → **全站 23 檔同步**(8 首頁 ＋ 3 總覽頁 ＋ 12 內容頁);
  子頁的錨點連結帶 `index.html` 前綴、同資料夾頁面用相對檔名。

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

- **微調現行風格**:改 `style-3-soc/` 內各頁的 tokens 與 CSS;共用內容全站同步、
  四組 A/B 跑 `<main>` diff(見一致性鐵則雙軸)。
- **改首頁版面變體**:變體檔**不要手改**——它們由腳本從 `index.html` / `index-nav-b.html`
  組出(hero / Built / Why / Trust / CTA 直接從現行首頁切片,確保跨變體逐字節相同)。
  改法:編輯產生腳本內的變體區塊後重跑,再跑雙軸檢查。腳本做法見 `HANDOVER.md` §版面變體。
  ⚠ V3 架構圖的三條硬約束:①不得用 `position:absolute`(768/390px 會崩,層間箭頭用
  `.stack>*+*` 的 normal-flow 元素);②承載語意的線條用 `--muted` 不用 `--line`
  (`--line #27344A` 在 `--bg` 上只有 **1.47:1**,不到 WCAG 1.4.11 的 3:1);
  ③箭頭字元用 `aria-hidden="true"` 的真字元,**不要**放進 `::before content`,
  也**不要**用 `role="img"` 包整張圖(會把裡面的連結對輔助科技隱藏)。
- **調整選單**:項目與分類名以本檔 0731 決議為準;GCP 產品名以 `docs/GCP_Introduce.md`
  (2026-08-03 查證、08-04 補 Cloud Armor)為準。
  ⚠️ **選單動到就是全站 23 檔同步**——手改必定漏,
  用腳本產生後跑 §驗證方式(既往腳本在 scratchpad,做法見 `docs/Cloud線_內容規劃_20260804.md` §7)。
  Nav B 的 flyout 顯示規則必須用**子代選擇器**(`.dd:hover>ul` 等),
  後代選擇器會讓巢狀層全開;且 Nav B 的 `.dd ul` **絕不可加 overflow**(會裁掉 flyout)。
- **補產品頁**:複製 `style-3-soc/sentinelone.html` → 改 `<title>`、meta description、
  eyebrow 索引碼、內容區塊;素材見 `docs/product/`(內部,先讀產品簡介總覽.md)。
  **模板四坑**:①`aria-current="page"` 搬到自己的 nav 項(Cloud 分類頁則掛頂層「Google Cloud」)、
  ②語言切換 EN 的 href 改自己檔名、③換成真連結的項刪 `title="Demo:…"`、
  ④`cards2` 必須偶數張(產品數為奇數時,把產品清單改走 `loglist`,`cards2` 留給沃凱交付項)。
  完成後全站 23 檔的導覽列/頁尾對應項換真連結。
- **補 Cloud 分類頁**:內容正本是 `docs/Cloud線_內容規劃_20260804.md`(§4 骨架、§5 逐項英文文案、
  §6 逐頁大綱);產品事實一律出自 `docs/GCP_Introduce.md`,不得自行擴充未查證的產品。
  每個產品在名冊 `loglist` 佔一列且**必須帶 `id`**(nav 深連結的落點),
  新頁必含 `main [id]{scroll-margin-top:80px}`,否則 66px sticky header 會蓋住落點。
- **版面定稿後**:勝出方案的內容搬進 `index.html`(對照組位置),落選的三個版面檔移入 `archive/`
  (或依使用者指示刪除);首頁檔數從 8 收斂回 2(Nav A/B),一致性鐵則的軸 2 隨之退場。
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
cd style-3-soc
# 軸1:四組「同版面 Nav A ↔ Nav B」自 <main> 起逐字節相同 → 四組皆應無輸出
for v in "index:index-nav-b" "index-v1-proof:index-v1-proof-nav-b" \
         "index-v2-catalogue:index-v2-catalogue-nav-b" "index-v3-flow:index-v3-flow-nav-b"; do
  a=${v%%:*}; b=${v##*:}; echo "== $a vs $b"
  diff <(awk '/<main>/,0' $a.html) <(awk '/<main>/,0' $b.html)
done
# 軸2:五句定稿文案在 8 個首頁全數命中 → 每句皆應輸出 8
while IFS= read -r s; do printf '%3d  %s\n' "$(grep -Fl "$s" index*.html | wc -l)" "${s:0:52}"; done <<'EOF'
from one turn-key partner.
one point of accountability.
One partner accountable for the whole stack.
we will map the path to cloud, security and operations.
Cloud, security and managed operations for European organisations.
EOF
# 核心句只在三變體 → 應輸出 6(對照組 index.html / index-nav-b.html 刻意不含)
grep -Fl 'We operate what we sell, and we build what we cannot buy.' index-v*.html | wc -l
# CTA 一律 Contact us(sentence case);禁 Contact Us、禁 Request a proposal(那是 style-4 的刻意變因)
grep -oh 'Contact us\|Contact Us\|Request a proposal' *.html | sort | uniq -c
# 死連結:每檔應只剩語言切換的 1 個
grep -c 'href="#"' *.html
# 「繁中」每筆同行都要有 lang 屬性 → 應輸出 0
grep -h '繁中' *.html | grep -vc 'lang="zh-Hant-TW"'
# 舊選單術語不得殘留 → 每檔應輸出 0
grep -c 'Arsenal\|>Platform<\|>Operations<' *.html
# 佔位連結歸零 → 每檔應輸出 0(改連真頁後不該再有頁尾錨點動線)
grep -c '#security-list\|#managed-list' *.html
# title 與 meta description 全站唯一 → 兩行皆應無輸出(註解宣稱兩項,指令就有兩條)
grep -h '<title>' *.html | sort | uniq -d
grep -h 'name="description"' *.html | sort | uniq -d
# aria-current 每檔=3(1 個 markup + 2 個 CSS 選擇器);markup 在首頁=Home、子頁=自己的 nav 項
grep -c 'aria-current="page"' *.html
# ess.html 與 services.html 零外部連結 → 皆應輸出 0
grep -c 'https\?://' ess.html services.html
# 錨點偏移:每檔應 ≥1(缺了的話 sticky header 會蓋住 #錨點 落點)
grep -c 'scroll-margin-top' *.html
# V3 圖中連結的鍵盤焦點不被遮蔽 → 兩檔應各為 1
grep -c '\.stack a{scroll-margin-top' index-v3-flow*.html
# Cloud 深連結落點:22 個錨點 id 必須存在(18 GCP 產品 + Cloud Armor + 沃凱服務 3 項)
grep -ohE 'id="(compute-engine|kubernetes-engine|vmware-engine|cloud-storage|filestore|backup-dr|bigquery|pubsub|dataflow|cloud-run|app-engine|api-gateway|alloydb|cloud-sql|datastore|firestore|vertex-ai|model-garden|cloud-armor|cloud-migration|hybrid-cloud-backup|data-ai-engineering)"' \
  cloud*.html | sort -u | wc -l   # 應為 22
# 兩個新總覽頁的落點:cybersecurity 8 產品 + 3 區塊、services 6 服務
grep -ohE 'id="(sentinelone|threatsonar|fortiedr|cybereyes|google-secops|ce-bas|ai-ptaas|secpurple)"' cybersecurity.html | sort -u | wc -l  # 應為 8
grep -ohE 'id="(edr|detection|in-house)"' cybersecurity.html | sort -u | wc -l   # 應為 3
grep -ohE 'id="(ess|soc|isms|pentest|finops|dx)"' services.html | sort -u | wc -l # 應為 6
# 14 個內容頁 footer 與 sentinelone 逐字節相同 → 應輸出 14 行 OK(排除 8 個 index*.html 與 sentinelone 自己)
for f in $(ls *.html | grep -vE '^(sentinelone|index.*)\.html$'); do
  diff <(awk '/<footer/,/<\/footer>/' sentinelone.html) \
       <(awk '/<footer/,/<\/footer>/' $f) >/dev/null && echo "$f OK" || echo "$f DIFF"; done
# 相對連結存在性(根 + style-3 共 24 檔)可用 python 一次掃:每個 href 的檔案與 #id 都要存在
```
