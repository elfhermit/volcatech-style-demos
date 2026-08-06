# CLAUDE.md — Volcatech 官網 Demo 專案指示

> 本檔由 Claude Code 自動讀取。接手本專案的任何 AI 助手與開發者都應遵守以下規則。

## 回覆語言

一律以繁體中文回覆;程式碼、指令、專有名詞與技術術語保留原文。

## 這個專案是什麼

沃凱科技(Volcatech)新官網的 demo 專案。**2026-07-31 內部評選已結束**,勝出組合為
**style-3-soc(SOC Console 深色色系)× 原版直落版型**,色系凍結。
**2026-08-05 會議又定案三件事**(結算正本:`docs/meeting_0805_end.md`):

1. **首頁收斂為 2 檔**:`index.html`(現行版)與 `index-v1-proof.html`(V1 信任前置)。
   V2/V3 與所有 Nav A/B 對照版共 6 檔已封存到 `archive/style-3-homepage-variants/`。
2. **選單改成三層、第一層不可點**、全站統一 Nav B(二層 flyout),不再有 Nav A。
3. **內容頁要改版**(區塊化、顏色區分、箭頭表關聯)。**2026-08-06 定案:走守硬性規則的
   inline CSS 版**(`lab/` 的 Tailwind 版落選),16 個內容頁與首頁已全數改用區塊元件,
   詳見下方〈內容頁區塊元件〉與〈軸 3〉。

現行 `style-3-soc/` 共 **36 頁**:2 首頁 ＋ 3 總覽 ＋ 7 Cloud 分類 ＋ 4 資安產品 ＋ 1 方案(ESS)
＋ **19 GCP 產品頁**(0806 補齊,選單第三層)。

**2026-08-06 第二輪**又定案四件事(來源:對 `docs/meeting_0805_end.md` 的逐條盤點,
決策記錄在 `docs/adr/`,術語正本在 `docs/CONTEXT.md`):

1. **區分不靠顏色**(ADR 0001)——會議說「用不同顏色區分」,但維持色系凍結,
   區分仍只靠三層表面深度 ＋ 琥珀邊界 ＋ 箭頭。
2. **Cloud 總覽兩層都留**(ADR 0002)——六領域卡 ＋ 19 產品索引。
3. **19 個產品頁全部建**(ADR 0003)——不再有「部分產品點得進去」的落差。
4. **不做互動式 comment 站**——會議原話「做不到就先 pass 沒關係」。做得到,
   但唯一不動硬性規則的做法是「連到預填標題的 GitHub Issue」(零 JS、零 CDN、零追蹤);
   內嵌 giscus/utterances 要載外部 script 與第三方 cookie,會賠掉整個 demo 的 GDPR 前提。
   本輪選擇維持現況(會議記錄 ＋ 口頭)。要做的話只能開在 `lab/`,不得進 `style-3-soc/`。

**首頁兩案**

| 方案 | 檔名 | hero 之後第一眼 |
|---|---|---|
| 現行(對照組) | `index.html` | Built → Why → Trust → Vendors(六個純文字) |
| V1 信任前置 | `index-v1-proof.html` | **How we work** 三步驟 → Trust 四項(資料主權/存取控制) → Partners 六張能力卡 |

V1 **不得手改**——由 `docs/reports/build_v1_20260806.py` 從 `index.html` 切片產生
(共用區塊 hero / Built / Why / Trust / CTA 直接取自現行首頁,確保逐字節相同)。
V1 專屬區塊代號:`#how`(交付三步)、`#partners`(夥伴)、`#catalogue`(服務索引)。
核心句 `We operate what we sell, and we build what we cannot buy.` 只在 V1 出現
(**對照組刻意不含**,它代表「今天線上的樣子」,不得為了湊一致而修改)。
- **GCP 產品頁 19 頁**(2026-08-06 補齊,選單第三層):18 個 GCP 產品各一頁,
  ＋ `gcp-cloud-armor.html`(孤兒頁,見下)。由 `docs/reports/build_gcp_pages_20260806.py`
  以 `cloud-compute.html` 為底檔產生(head / tokens / header / footer 全部沿用,只換 `<main>`)。
  **骨架與資安產品頁不同**:Hero →核心優勢 3 卡(`trio`,自繪 SVG icon)→關鍵特色(`spec` 深色面板
  ＋mono 編號)→適用場景(`uses`,琥珀左邊界)→ Works with(`stack`＋`flowmark` 真箭頭)→ CTA。
  刻意**不含**「痛點／成效／沃凱交付 4 卡」——那三區需要沃凱觀點素材,目前完全沒有。
  **不做頁籤**(0805 決策):Key features 與 Use cases 平鋪成兩個 section,可深連結、Ctrl+F 找得到。
  檔名用 `gcp-` 前綴,避免與分類頁的 `cloud-*` 撞前綴、也避開錨點檢查的 `cloud*.html` glob。
  文案正本 `docs/GCP_Introduce_v2.md`(**19 個產品全部有素材**,每產品 7 欄位;
  舊版 CLAUDE.md 說「約 5 個產品素材太薄」已於 0806 實測推翻,唯一破格的是 Model Garden——
  它沒有「關鍵特色」欄,改為模型清單)。改寫三原則:英式拼寫、
  **刪原廠量化宣稱**(4x／11 個 9 之類)、刪 `autonomous`/`AI-ready`/`unified` 這類自我定位詞。
  每頁的 `stack` 都必須有一個**沒有 href 的自我節點**(渲染成 `.node.self`),否則圖裡看不出主角是誰。
  `stack` 的節點一律連 `gcp-*.html`,不再連「分類頁#錨點」。
- 資安產品頁:`sentinelone.html`、`threatsonar.html`、`cybereyes.html`、
  `google-secops.html`(2026-08-03 依 `docs/product/` 內部素材新建);另有方案頁 `ess.html`
  (ESS=沃凱打包方案 WDR+EDR+7x24 SOC,非 19 項 SKU;**全頁零外部連結**,入口在 Services 下拉)。
- **Cloud 線 8 頁**(2026-08-04 新建,內容正本= `docs/Cloud線_內容規劃_20260804.md`):
  `cloud.html`(總覽,CI)＋六個 GCP 分類頁 `cloud-compute` / `cloud-storage` / `cloud-analytics` /
  `cloud-serverless` / `cloud-databases` / `cloud-ai`(CI-01〜CI-06)＋
  `cloud-services.html`(CI-07,Cloud Armor＋沃凱雲端服務 3 項)。
  **分類頁骨架**(0806 區塊化後的現況):`#pain`(`probs`)→ 產品區(`trio`/`quad`/`duo`,
  **每張產品卡帶 `id` 當深連結落點**)→ `#delivery`(`steps` 或 `quad`)→ `#outcomes`(`spec`)→ `#why`。
  ⚠ 舊版本檔說產品走「名冊 `loglist`」——**那是 0806 改版前的狀態**,`loglist` 現在只用在
  `cloud.html` 的產品索引,分類頁的產品一律是卡片。`cards2` 同樣已退場。
  每張產品卡有**兩個出口**(`.goes` 併成一列):站內 `Product page →` 在前、
  離站 `Vendor page ↗`(帶 `target="_blank" rel="noopener"`)在後。這兩條由
  `link_products_20260806.py` 產生,不要手改。
  **代碼分層**:`CI-*` 是頁面層(現行);`C-*`/`E-*`/`S-*`/`X-*` 是 SSOT §A 的 SKU 層,
  已於 2026-08-04 定案為 **pre-0731 歷史體系**,不對齊、不上站。
- 選單分類已依會議決議由 Platform / Arsenal / Operations 改為
  **`Google Cloud` / `CyberSecurity` / `Services`**(`CyberSecurity` 駝峰是會議指定的刻意寫法,
  勿「順手修正」成 Cybersecurity;正文與板塊名仍用 Cybersecurity)。
  **選單的唯一正本是 `docs/reports/rebuild_nav_20260806.py` 的 `MENU` 常數**,不是任何 HTML 檔。
  改選單 = 改那個常數後重跑腳本,再跑 `check_nav_20260806.py`。手改必定漏。

**選單結構(2026-08-06 起,三層)**

- **第一層不可點**:三個分類是 `<button type="button" aria-haspopup="true">`,不是 `<a>`。
  用 button 而非 span 是為了保留 keyboard focusable,`:focus-within` 才會生效、不需要 JS。
  **button 的 CSS 重設必須含 `padding:8px 0` 與 `line-height:inherit`**——`.menu a` 選不到 button,
  少了它 `<li>` 會變矮、面板上移、滑鼠往下移時出現空隙導致面板閃退。
  `.dd>a::after` 也必須寫成 `.dd>a::after,.dd>button::after`,否則三個下拉三角形全消失。
- **第二層**= 分類頁(Google Cloud 六組指向 `cloud-*.html`;CyberSecurity 三組指向
  `cybersecurity.html#錨點`);**第三層**= 產品。
- Google Cloud:Overview → `cloud.html`,六組 18 項,**18 項全部連各自的 `gcp-*.html` 產品頁**
  (0806 補齊,不再有「分類頁#錨點」的過渡狀態)。
  產品資料正本 `docs/GCP_Introduce.md`(2026-08-04 補第 7 節 Cloud Armor)。
- CyberSecurity:Overview ＋ Endpoint—EDR(SentinelOne / ThreatSonar / **FortiEDR 灰字**)、
  Detection—SIEM & WDR(CyberEyes / Google SecOps)、
  Built in-house—Volcatech AI Security(CE-BAS)。WDR 併記是因 CyberEyes 實為 WDR。
- Services(扁平,無第二層):Overview ＋ ESS ＋ 24/7 SOC & IR ＋ **GCP Managed Services 灰字**。
- **灰字項**(`<span class="off">`,附 mono 的 Coming soon)= 尚無內頁的項目,刻意不可 focus。
  用 `--muted` 上色(對 `--surface` 6.79:1,過 AA)。**絕不可寫成 `<a href="#">`**——
  會踩到「每檔只能有 1 個 `href="#"`」的檢查。
- 每個下拉第一行保留 mono 白話對照(`li.head`)。
- ⚠️ **`.dd ul` 絕不可加 overflow** —— 會變成 clip container 裁掉二層 flyout。
  Nav B 的第一層面板最多 8 列,不需要捲動(Nav A 時代的 `max-height`/`overflow-y` 已隨 Nav A 一起退場)。
- ⚠️ **`.sub` 的四條規則一律 scope 成 `.menu .sub`** —— footer 有內文用的 `<p class="sub">`。
- ⚠️ 901–1100px 這一段,二層改成**在面板內就地展開**(`position:static`),不是側開 flyout:
  該區間視窗放不下側開的 flyout,窄端會跑出左緣。

**0805 從選單移除的 6 項(只動選單,頁面區塊全部保留)**

CyberSecurity 的 `AI-PTaaS`、`SecPurple`;Services 的 `ISMS / PIMS`、`Penetration Testing`、
`Cloud FinOps`、`Digital Transformation`。這六項在 `cybersecurity.html` / `services.html` 的
區塊與頁尾清單一律照舊,只是不出現在下拉裡。同理 0805 移除的 `Edge security`(Cloud Armor)與
`Volcatech cloud services` 兩組——`cloud-services.html` 頁面與頁尾那列都還在。
**首頁的 Built by Volcatech 仍須列出 CE-BAS / AI-PTaaS / SecPurple 三品**(硬性規則),不受選單影響。

評選期的 4 個色系風格(style-1/2/4)、4 個版型變體(layout-1〜4)、外部 AI 參考組,
以及 0805 封存的 6 個首頁變體檔(`archive/style-3-homepage-variants/`)
已全部**凍結封存於 `archive/`**(封存總覽= `archive/index.html`),一律不再修改;
根 `index.html` 是 Demo hub:首屏講本輪落地了什麼,下方依序為兩個首頁方案、兩個總覽頁、
style-3 全部內容頁、**lab/ 內容頁改版提案**、歷史存檔入口。
兩個首頁檔底部有 backlink 切換列(`Layout: Current · V1`),比較時不必回 hub。

- 目標受眾:歐洲企業的 IT / 資安決策者;語言英文為主(正式版另有繁中 /zh-tw/,架構須可擴充更多語系)
- 新官網將**改版取代**現有 volcatech.com
- 公司事實唯一可信來源:`docs/公司_104.md`(僅可用於服務範圍與願景,**不可**用來填統編/VAT/地址)。
  ⚠️ 2026-08-04 使用者指示**本次先不參考它**,0806 再次確認維持——沃凱自有服務描述一律 `[TODO]`,
  待新素材;各頁交付卡是不含獨有宣稱的通用交付項,取得素材後須校正。
- 下一步:①**兩個首頁二選一**(現行版 vs V1);②`cloud-services.html` 的沃凱服務 3 段內文待素材;
  ③每個 `gcp-*.html` 的 `[TODO: delivery model and response times]` 同樣待素材;
  ④補齊 Services 線其餘服務頁;⑤全站頁尾的法定資訊(統編/VAT/地址/Email/電話)待公司提供;
  ⑥再依 `docs/Volcatech_多風格_Build_Prompts.md` 的「共用基底 + 勝出風格模組」
  產生正式 **Astro** 版(雙語 i18n、GDPR 隱私頁、sitemap/hreflang)
  ~~決定其餘 15 個 GCP 產品頁做不做~~、~~cloud.html 要不要展開成產品層~~ 已於 0806 完成。
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
| Nav 結構 | 三層:`Google Cloud ▾ / CyberSecurity ▾ / Services ▾`(第一層是不可點的 `<button>`)→ 分類頁 → 產品;每個下拉首行為 mono 白話對照;二層 flyout(`.menu .sub`,一律子代選擇器 `>`) |

額外禁止事項(評選期規則,仍適用):無 glow、無純黑、琥珀不得用於連結與小字、正文禁 ALL CAPS
(mono 微標籤如 `li.head`/`.off .soon`/status 行不在此限)。
歷史四風格的 tokens 對照見 `archive/index.html` 或 `docs/Volcatech_多風格_Build_Prompts.md` §B。

### 內容頁區塊元件(2026-08-06,全站 36 頁共用)

0805 的意見是「每頁都是同一個 `loglist` 重複三四次,讀起來是一整欄沒分別的文字」。
現在每一段各有自己的處理,眼睛在讀字之前就分得出它是哪一類:

| class | 語意角色 | 長相 |
|---|---|---|
| `.probs` / `.uses` | 痛點(專案前的狀態)／場景(為了什麼情境) | `--surface` ＋ 3px 琥珀左邊界;四項時加 `.four` |
| `.trio` / `.quad` / `.duo` | 產品、服務、能力卡 | `--surface` 卡 ＋ 自繪 SVG icon ＋ 可選 `.go` 連結;3／4／2 欄 |
| `.steps` | **有先後順序**的流程 | `#111A26` 節點 ＋ `--muted` 邊框 ＋ 節點間的真箭頭 |
| `.spec` | 事實／規格／成效清單 | `#111A26` 深色面板 ＋ mono 兩位數編號 |
| `.stack`＋`.layer`＋`.node`＋`.flowmark` | 分層架構圖(目前只在 `gcp-*.html`) | 分層方塊 ＋ 真箭頭 |
| `.loglist` | 緊湊索引(目前只在 `cloud.html#products`) | 帶邊框的單欄列表 ＋ 狀態圓點 |
| `.goes` | 一張卡有兩個出口時的連結列 | 把兩個 `.go` 併成一列,不讓它們各佔一行 |

**唯一正本是 `docs/reports/restyle_content_20260806.py` 的 `BLOCK_CSS`**(含 35 個自繪 icon 的
`ICONS` 常數)。改元件樣式 = 改那個常數後重跑腳本,36 檔一次同步;**手改單頁的 CSS 會讓軸 1 立刻紅**。

四條硬約束:
1. **不得新增色票**——區分只靠三層表面深度(`--bg` / `--surface` / `#111A26`)、一道琥珀邊界、
   一列真箭頭。0731 的色系凍結仍然成立。
2. `.steps` **只能用在真的有先後順序的內容上**。四個並列項目硬插箭頭 = 假造推進關係,
   是這輪最容易犯的錯。判不出順序就用 `.quad`。
3. `stack` 的三條沿用 V3:①不得用 `position:absolute`(768/390px 會崩);②承載語意的線條用
   `--muted` 不用 `--line`(`--line` 對 `--bg` 只有 **1.47:1**,不到 1.4.11 的 3:1);
   ③箭頭用帶 `aria-hidden="true"` 的真字元,不放進 `::before content`。
4. icon 一律**從 `ICONS` 挑**,不自繪新的、不引外部 icon 套件、不用 `<img>`;同一頁不得重複。

hover 有 2px 浮起 ＋ 邊框變色(**不加陰影**,專案禁 glow),`prefers-reduced-motion` 下關閉。

## 一致性鐵則:三軸

⚠️ **舊軸 1(Nav A ↔ Nav B 自 `<main>` 起逐字節相同)已於 2026-08-06 退場**——首頁收斂為 2 檔、
全站統一 Nav B 之後,A/B 對照物理上不存在了。它曾是全站**唯一**能自動抓到「手改漏一檔」的檢查,
所以必須有東西接手,新軸 1 就是那個接手的東西。

### 軸 1|全站 header 同源:正規化後 36 檔逐字節相同

`python3 docs/reports/check_nav_20260806.py` → 必須 PASS。

它把每檔的 `<header>` 與**四段 CSS**(三段 nav ＋ 0806 的區塊元件)取出,
正規化掉 5 個本來就該逐檔不同的參數
(EN 自指 href、logo/Home 目標、About/Contact 的錨點前綴、`aria-current` 落點、`class="on"` 落點)
之後,要求 **36 檔逐字節相同**;另外檢查結構數量(`li.sub`=9、`li.head`=3、button=3、
`.off`=2、`li.grp`=0)、`aria-current` 落點、Esc handler、以及 `.dd ul` 沒有 overflow。

- **`aria-current="page"` 掛「選單裡 href 等於本檔名的那個 `<a>`」**,通常在第二層。
  第一層是 button,`.menu a[...]` 選不到它——所以視覺上的「你在這個區塊」改用
  `class="on"`(非 ARIA)掛在 button 上。這兩個角色不可混用。
- **孤兒頁登記**:選單裡沒有任何連結指向它的頁面,header 內就沒有 `aria-current`。
  目前有兩個:`cloud-services.html`(0805 兩組移出選單所致)與 `gcp-cloud-armor.html`
  (0806 補齊產品頁時一併產出,但它所屬的 Edge security 那組已被移出選單)。
  **孤兒必須明文登記在 `check_nav_20260806.py` 的 `ORPHANS`**,不能默默出現——腳本會擋。
  孤兒頁的第一層 `.on` 仍要亮,所以也要在 `rebuild_nav_20260806.py` 的 `SECTION` 補一筆
  (`SECTION` 的其餘部分由 `MENU` 自動推導,不手維護)。
- 基準用**多數決**而非「第一個檔」:破壞若落在第一個檔,否則報告會反過來指控其餘 19 檔。

### 軸 2|兩個首頁的共用文案逐字凍結

不要求結構相同(結構就是變因),但共用文案必須逐字一致,否則會變成比文案而不是比版面
(踩過的坑:全域教訓簿 2026-07-30)。**凍結清單**:

| 句子 | 應命中的首頁檔數 |
|---|---|
| `Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`(H1) | 2 |
| `…deploy and tune EDR and SIEM… one point of accountability.`(副標) | 2 |
| `One partner accountable for the whole stack.`(Why H2) | 2 |
| `Tell us about your environment — we will map the path to cloud, security and operations.`(CTA) | 2 |
| `Cloud, security and managed operations for European organisations.`(footer 品牌句) | 2 |
| `We operate what we sell, and we build what we cannot buy.`(核心句) | **1**(僅 V1) |

最後一句刻意只在 V1 出現——`index.html` 是**未經內容改動的對照組**,
代表「今天線上的樣子」,不得為了湊一致而修改它。
(0806 的區塊化只改版型,`index.html` 的**文案**仍未經改動,對照組的意義成立。)

### 軸 3|內容頁改版型時文案零漂移

`python3 docs/reports/check_copy_20260806.py` → 必須 PASS。

它拿 git 基準版(預設 `HEAD`)與工作區各自抽出 `<main>` 的文字節點比對集合:
**任何一句消失都是 FAIL**;新增只允許三類——`.go` 連結標籤(結尾帶 `→`/`↗`)、`.steps` 的箭頭、
`.spec`/`.steps` 的兩位數編號。

為什麼需要它:0806 一次改 16 頁的 `<main>`,而全域教訓簿 2026-07-30 那條的教訓是
「同一份內容分散在多檔各自被順手改過,比較就從比版面變成比文案」。改版型的價值同樣會被
這種漂移吃掉——讀的人分不出「這頁比較好懂」是因為版型還是因為字被改順了。

⚠️ 它的基準是 **git**,所以 **commit 之後基準就前進了**。要對更早的狀態比,傳 ref:
`python3 docs/reports/check_copy_20260806.py <commit>`。**真的要改文案時**,
改完 commit,之後的檢查自然以新文案為基準。

### 共同規則

- 兩個方案的 **hero 區塊(`#top` 含 `#offer` 三張卡)完全相同**,差異一律從第二區塊開始。
- 改任何共用內容(hero、Built、Why、Trust、footer)→ 改 `index.html` 後
  **重跑 `docs/reports/build_v1_20260806.py`**,V1 會自動跟上。
- 動到 nav 項目 → 改 `rebuild_nav_20260806.py` 的 `MENU` 後重跑,**全站 36 檔一次同步**;
  動到 footer 清單 → 36 檔都要改(footer 目前沒有產生器,靠逐字節比對把關)。
  子頁的錨點連結帶 `index.html` 前綴、同資料夾頁面用相對檔名。

## 實驗區:`lab/`(已定案,留檔備查)

2026-08-06 新增,同日定案。**結果:選 inline CSS 版**,元件已搬進 `style-3-soc/` 全部 36 頁
(正本 `docs/reports/restyle_content_20260806.py`)。這個資料夾自此只剩紀錄價值——
它保存了「當初為什麼沒選 Tailwind」的實際對照,**隨時可整個刪掉**,刪除時機由專案負責人決定。
目前四個檔:
`index.html`(比對入口,三欄對照表)、`inline-cloud-compute.html`(守硬性規則的分類頁改版提案)、
`tailwind-cloud-compute.html`、`tailwind-cloud-run.html`(照 0805 prompt 的 Tailwind 實驗版)。

1. **`lab/` 的規則與 `style-3-soc/` 不同,而且只在 `lab/` 內有效。**
   兩個 Tailwind 頁**刻意違反**禁外部 CDN、禁框架、色系凍結三條硬性規則——那正是要被看見的成本。
   它們頂端都有醒目橫幅說明,`lab/index.html` 也重複一次。
2. **不得擴散**:`style-3-soc/` 的任何一頁都不准出現 Tailwind、外部 CDN 或淺色色票。
3. **已定案(0806)**:走 inline 版,做法已搬回 `style-3-soc/`。**當初就不是把 `lab/` 的檔案
   搬過去**,而是把元件抽成共用 CSS 正本後逐頁重寫 `<main>`。`lab/inline-cloud-compute.html`
   的 `<main>` 即現行 `style-3-soc/cloud-compute.html` 的來源(路徑已還原)。
4. 提案頁的文案與被比對的頁面**逐字相同**,只有版型不同——否則會變成比文案而不是比版型
   (踩過的坑:全域教訓簿 2026-07-30)。

## 封存區:`archive/`(唯讀,平常不動它)

**是什麼**:0731 評選結束後封存的全部評選材料——`style-1-zurich/`、`style-2-nordic/`、
`style-4-continental/`、`layout-1〜4/` 四個版型變體、外部 AI 參考組
`Volcatech_Layout_Variants_GPT/`,與當時的評選總覽 `archive/index.html`(帶已歸檔橫幅);
外加 2026-08-05 收進來的 **`style-3-homepage-variants/`**(V2/V3 與四組 Nav A/B 對照版共 6 檔)。
那 6 檔因為下移一層,相對連結已由 `docs/reports/archive_homepage_variants_20260806.py`
重指回 `../../style-3-soc/`,可以正常瀏覽;它們的選單是**改版前的兩層結構**,不代表現況。

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

**每一項的最後一步都一樣:跑 §驗證方式 的三條指令(check_nav、連結掃描、內容檢查)。**

- **微調現行風格**:改 `style-3-soc/` 內各頁的 tokens 與 CSS。動到 nav CSS 就必須用
  `rebuild_nav_20260806.py`(改 `CSS_DESK` / `CSS_MOB` / `CSS_1100` 三個常數之一)重跑,
  手改單檔會讓軸 1 立刻紅。
- **調整選單**:**唯一正本是 `rebuild_nav_20260806.py` 的 `MENU` 常數**。改它 → 重跑 →
  跑 `check_nav_20260806.py`。腳本可重複執行,已是新結構的檔會被跳過。
  GCP 產品名以 `docs/GCP_Introduce.md` 為準(2026-08-03 查證、08-04 補 Cloud Armor)。
  flyout 顯示規則必須用**子代選擇器**(`.dd:hover>ul` / `.menu .sub:hover>ul`),
  後代選擇器會讓巢狀層全開;`.dd ul` **絕不可加 overflow**(會裁掉 flyout)。
- **改 V1 首頁**:V1 **不要手改**——編輯 `build_v1_20260806.py` 內的 V1 區塊後重跑。
  改共用區塊(hero / Built / Why / Trust / CTA)則是改 `index.html`,再重跑腳本讓 V1 跟上。
- **補 GCP 產品頁**:在 `build_gcp_pages_20260806.py` 的 `PAGES` 加一筆後重跑,
  再跑一次 `rebuild_nav_20260806.py`(新頁的 header 才會拿到正確的 `aria-current` 與 `.on`)。
  並記得把 `MENU` 裡該產品的 href 從 `分類頁#錨點` 改成新頁檔名。
  文案正本 `docs/GCP_Introduce_v2.md`;**不得自行擴充未查證的產品事實**。
- **補資安產品頁**:複製 `style-3-soc/sentinelone.html` → 改 `<title>`、meta description、
  eyebrow 索引碼、內容區塊;素材見 `docs/product/`(內部,先讀產品簡介總覽.md)。
  完成後跑 `rebuild_nav_20260806.py`(header 自動處理),並把 `MENU` 裡該項改成真連結。
  ⚠ `cards2` 必須偶數張(產品數為奇數時,把產品清單改走 `loglist`,`cards2` 留給沃凱交付項)。
- **補 Cloud 分類頁**:內容正本是 `docs/Cloud線_內容規劃_20260804.md`(§4 骨架、§5 逐項英文文案、
  §6 逐頁大綱);產品事實一律出自 `docs/GCP_Introduce.md`。
  每個產品在名冊 `loglist` 佔一列且**必須帶 `id`**(nav 深連結的落點),
  新頁必含 `main [id]{scroll-margin-top:80px}`,否則 66px sticky header 會蓋住落點。
- **改內容頁的版型**:元件樣式改 `restyle_content_20260806.py` 的 `BLOCK_CSS` 後重跑
  (36 檔一次同步);某一頁的 markup 則直接改該檔的 `<main>`。改完必跑
  `check_copy_20260806.py` 確認沒有把文案一起改掉。
  ⚠️ `.steps` 只能用在真的有先後順序的內容;判不出順序就用 `.quad`,不要為了版型假造推進關係。
- **版面定稿後**:勝出方案的內容搬進 `index.html`(對照組位置),另一個移入 `archive/`;
  首頁收斂為 1 檔,一致性鐵則的軸 2 隨之退場,`build_v1_20260806.py` 一併退役。
- **產生正式 Astro 版**:不要改造本 demo;在新資料夾/新 repo 依
  `docs/Volcatech_多風格_Build_Prompts.md`(基底 + style-3 模組,選單以 0805 決議覆蓋)執行,
  完成後跑該檔【品質底線(驗收)】清單(**不是** v3 的 §9,那份已失效)。

### `docs/reports/` 腳本現況(2026-08-06)

| 腳本 | 做什麼 |
|---|---|
| `rebuild_nav_20260806.py` | **選單唯一正本**。整段抽換 header ＋ 三段 nav CSS,可重複執行 |
| `restyle_content_20260806.py` | **區塊元件 CSS ＋ 35 個 icon 的唯一正本**。注入 36 檔,可重複執行 |
| `check_nav_20260806.py` | 軸 1 檢查:36 檔 header ＋ 四段 CSS 逐字節相同 ＋ 結構數量 ＋ 孤兒登記 |
| `check_copy_20260806.py` | 軸 3 檢查:對 git 基準逐句比對 `<main>`,文案零漂移 |
| `check_links_20260806.py` | 標籤配對、唯一 h1、id 不重複、相對連結與錨點有效 |
| `build_v1_20260806.py` | 從 `index.html` 產生 `index-v1-proof.html`(0804 那支改造而來) |
| `build_gcp_pages_20260806.py` | 產生 19 個 GCP 產品頁(以 `cloud-compute.html` 為底檔)。**產品文案的唯一正本** |
| `link_products_20260806.py` | 分類頁 19 張產品卡的雙出口連結 ＋ `cloud.html#products` 索引。可重複執行 |
| `build_lab_20260806.py` | 產生 `lab/inline-cloud-compute.html`(**已完成階段任務**,`lab/` 刪掉後可一併移除) |
| `archive_homepage_variants_20260806.py` | 封存 6 檔後的相對路徑修正 |
| ~~`sync_nav_20260804.py`~~ / ~~`remove_gcp_groups_20260805.py`~~ | **已封印**,檔頭 `sys.exit` 擋住。功能被 `rebuild_nav` 取代 |

## 檔案放置規約(維持根目錄乾淨)

**專案根 = 本檔所在目錄**(`/Users/shiro/Work/Volcatech_Web/`);CLAUDE.md、README.md 與 docs 內
所有相對路徑皆以此為基準。

| 要放什麼 | 放哪 |
|---|---|
| 規劃書、需求、prompt 集、會議記錄 | `docs/` |
| **詞彙表**(同一個詞被用來指不同東西時的正本) | `docs/CONTEXT.md`(不放專案根——根目錄有白名單) |
| **決策記錄(ADR)**:難逆、意外、有真取捨的決定 | `docs/adr/NNNN-slug.md`,編號遞增 |
| 一次性腳本、比對報告、體檢輸出 | 臨時 → scratchpad;要保留 → `docs/reports/`(檔名帶日期) |
| 現行風格的頁面與資產 | 只在 `style-3-soc/` 內 |
| **改版提案 / 技術實驗**(未定案、不上正式版) | `lab/`,見下方專節 |
| 評選期封存材料(含外部 AI 參考組) | `archive/`,凍結不動 |
| 勝出風格的正式 Astro 版 | 新資料夾 `site/`,**不改動本 demo** |
| 第三方 agent skills(僅本機,不進版控) | `.claude/skills/`;來源與版本記於其內 `SOURCES.md`,使用指南見 `docs/skills_使用指南_20260806.md` |
| 制度檔(本檔、HANDOVER.md 等)修改前的備份 | `docs/backups/`,檔名加 `.bak-YYYYMMDD`(即全域維護協議所稱「專案備份目錄」的本專案對應) |

根目錄只允許:`index.html`、`README.md`、`CLAUDE.md`、`HANDOVER.md`、`.gitignore`、`.nojekyll`
與上表資料夾(`.vscode/`、`.github/`、`.claude/` 除外)。**不要在根目錄新增散檔**;
`.DS_Store` 等系統檔已由 `.gitignore` 排除。

根目錄文件分工:`README.md` = 對外接手指南(本機預覽與 GitHub Pages 部署步驟的正本、專案結構圖);
`HANDOVER.md` = 進度與交接速查(規格正本仍在 `docs/`);
`.github/copilot-instructions.md` = 本檔硬性規則的濃縮副本(供 GitHub Copilot 使用者)。

**版控範圍**:demo 推到 public repo 供瀏覽,`docs/` 與 `.claude/` 已列入 `.gitignore`
(內部建置計畫與本機 skills 不對外),因此**頁面內不得連結 `docs/` 內的檔案**,否則線上會是死連結。
`.nojekyll` 用於關閉 GitHub Pages 的 Jekyll 處理,勿刪。

## 驗證方式(改完必做)

> **檢查範圍**:根 `index.html`、`style-3-soc/`、`lab/`。
> `archive/` 是凍結封存區,**不在檢查範圍內**——下列指令的 glob 刻意不涵蓋它,
> 不要為了湊「全站掃過」而把它加進去(理由見上方 archive 專節)。

### 三支腳本先跑,都必須 PASS

```bash
python3 docs/reports/check_nav_20260806.py     # 軸 1:36 檔 header ＋ 四段 CSS 同源、結構數量、孤兒登記
python3 docs/reports/check_copy_20260806.py    # 軸 3:改版型沒把文案一起改掉(基準預設 HEAD)
python3 docs/reports/check_links_20260806.py   # 標籤配對、唯一 h1、id 不重複、相對連結與錨點
```

### 內容檢查(改過 style-3 任何頁面後必跑)

```bash
cd style-3-soc
# 軸2:五句定稿文案在 2 個首頁全數命中 → 每句皆應輸出 2
while IFS= read -r s; do printf '%3d  %s\n' "$(grep -Fl "$s" index*.html | wc -l)" "${s:0:52}"; done <<'EOF'
from one turn-key partner.
one point of accountability.
One partner accountable for the whole stack.
we will map the path to cloud, security and operations.
Cloud, security and managed operations for European organisations.
EOF
# 核心句只在 V1 → 應輸出 1(對照組 index.html 刻意不含)
grep -Fl 'We operate what we sell, and we build what we cannot buy.' index*.html | wc -l
# 無外部資源請求 → 應為空(全站唯一 JS 是各頁 navbtn 的行內 onclick;不得新增 <script> 標籤)
grep -nE '<img |<script|@import|<link ' *.html
# 外連只該是原廠 anchor,且同行有 rel="noopener" → 應為空
grep -n 'https\?://' *.html | grep -v 'rel="noopener"'
# CTA 一律 Contact us(sentence case);禁 Contact Us、禁 Request a proposal
grep -oh 'Contact us\|Contact Us\|Request a proposal' *.html | sort | uniq -c
# 死連結:每檔應只剩語言切換的 1 個。灰字項絕不可寫成 <a href="#">,一寫這條就紅
grep -c 'href="#"' *.html
# 「繁中」每筆同行都要有 lang 屬性 → 應輸出 0
grep -h '繁中' *.html | grep -vc 'lang="zh-Hant-TW"'
# 舊選單術語不得殘留在「選單」→ 應輸出 0
# ⚠ 只能掃 header 區。Platform 在正文是合法英文字——gcp-vmware-engine / gcp-vertex-ai /
#   gcp-model-garden 的架構圖層名就叫 <h3>Platform</h3>,掃全檔會誤報這三頁(0806 實測)
for f in *.html; do awk '/<header/,/<\/header>/' $f; done \
  | grep -c 'Arsenal\|>Platform<\|>Operations<\|<li class="grp">'
# 19 張產品卡都有兩個出口 → 兩行皆應輸出 19
grep -oh 'Product page →' cloud-*.html | wc -l
grep -oh 'Vendor page ↗' cloud-*.html | wc -l
# 每個產品頁的架構圖都要標出主角 → 19 個 gcp 頁各 1(輸出應為空)
grep -c 'node self' gcp-*.html | grep -v ':1$'
# cloud.html 的產品索引 19 列
grep -c 'Product page →' cloud.html
# 0805 移除的 6 項:選單裡應為 0,但頁面區塊必須還在(所以只能掃 header 區,不能掃全檔)
for f in *.html; do awk '/<header/,/<\/header>/' $f; done \
  | grep -c 'AI-PTaaS\|SecPurple\|ISMS\|Penetration Testing\|Cloud FinOps\|Digital Transformation'
# 佔位連結歸零 → 每檔應輸出 0
grep -c '#security-list\|#managed-list' *.html
# title 與 meta description 全站唯一 → 兩行皆應無輸出(註解宣稱兩項,指令就有兩條)
grep -h '<title>' *.html | sort | uniq -d
grep -h 'name="description"' *.html | sort | uniq -d
# aria-current 每檔=3(1 個 markup + 2 個 CSS 選擇器);cloud-services.html=2(登記在案的孤兒頁)
grep -c 'aria-current="page"' *.html
# ess.html 與 services.html 零外部連結 → 皆應輸出 0
grep -c 'https\?://' ess.html services.html
# 錨點偏移:每檔應 ≥1(缺了的話 sticky header 會蓋住 #錨點 落點)
grep -c 'scroll-margin-top' *.html
# 分層圖中連結的鍵盤焦點不被遮蔽 → 三個 GCP 產品頁應各為 1
grep -c '\.stack a{scroll-margin-top' gcp-*.html
# Cloud 深連結落點:22 個錨點 id 必須存在(18 GCP 產品 + Cloud Armor + 沃凱服務 3 項)
grep -ohE 'id="(compute-engine|kubernetes-engine|vmware-engine|cloud-storage|filestore|backup-dr|bigquery|pubsub|dataflow|cloud-run|app-engine|api-gateway|alloydb|cloud-sql|datastore|firestore|vertex-ai|model-garden|cloud-armor|cloud-migration|hybrid-cloud-backup|data-ai-engineering)"' \
  cloud*.html | sort -u | wc -l   # 應為 22
# 兩個總覽頁的落點:cybersecurity 8 產品 + 3 區塊、services 6 服務
grep -ohE 'id="(sentinelone|threatsonar|fortiedr|cybereyes|google-secops|ce-bas|ai-ptaas|secpurple)"' cybersecurity.html | sort -u | wc -l  # 應為 8
grep -ohE 'id="(edr|detection|in-house)"' cybersecurity.html | sort -u | wc -l   # 應為 3
grep -ohE 'id="(ess|soc|isms|pentest|finops|dx)"' services.html | sort -u | wc -l # 應為 6
# 33 個內容頁 footer 與 sentinelone 逐字節相同 → 應輸出 33 行 OK(排除 2 個 index*.html 與 sentinelone 自己)
for f in $(ls *.html | grep -vE '^(sentinelone|index.*)\.html$'); do
  diff <(awk '/<footer/,/<\/footer>/' sentinelone.html) \
       <(awk '/<footer/,/<\/footer>/' $f) >/dev/null && echo "$f OK" || echo "$f DIFF"; done
```

### 手動檢查(腳本抓不到的)

```bash
python3 -m http.server 8000   # 開 http://localhost:8000 逐頁檢查
```

1. **四種 `aria-current` 落點型態各開一頁,確認黃底線還在**:`cloud.html`(Overview 型)、
   `cloud-compute.html`(第二層型)、`sentinelone.html`(第三層型)、`gcp-cloud-run.html`(第三層新頁)。
   ⚠ `grep -c` 數的是行數不是語意——第一層換成 button 之後就算樣式壞了,它仍會回報正常。
2. **選單**:第一層不可點;斜著移進 flyout 不掉層;純鍵盤 Tab 全程可達;**按 Esc 面板關閉**。
3. **約 1000px 寬**:二層改成面板內就地展開,不會跑出畫面(這個區間 19 個原 Nav A 檔從沒測過)。
4. **390 / 768 / 1024 / 1440px** 無水平捲軸;390px 選單三層全部攤開成縮排清單。
5. 深色長文可讀性;對比用 DevTools 的 contrast checker。

## 已知缺口(明文登記,不含糊帶過)

demo 不宣稱「完全符合 WCAG 2.2 AA」。以下七項是知道且刻意留著的(前五項無障礙、後兩項一致性):

1. **SC 1.4.11 非文字對比**:下拉面板邊框用 `--line #27344A`,對 `--bg` 只有 **1.47:1**
   (面板底色對背景更只有 1.12:1),不到 3:1。2026-08-05 使用者裁決**這輪不修**,Astro 正式版處理。
2. **`aria-expanded` 刻意不寫**:純 CSS 無法同步。永遠是 `false` 的 `aria-expanded`
   比沒有更糟——它會主動對螢幕閱讀器撒謊。
3. **螢幕閱讀器瀏覽模式讀不到下拉**:`display:none` 把面板移出無障礙樹,方向鍵瀏覽
   不會觸發 `:focus-within`。資訊沒有遺失(三個 Overview 頁與 footer 都是下拉的平鋪版),
   但選單不是唯一入口。
4. **`aria-haspopup="true"` 是半真話**:它宣告的是 ARIA menu widget,期待 `role="menu"`
   與方向鍵巡覽,這份 markup 都沒有。全站沿用已久,維持現狀但記錄在案。
5. **`lab/` 兩個 Tailwind 頁使用外部 CDN**:GDPR 前提在該資料夾不成立,
   且斷網時會退化成無樣式 HTML。僅供內部視覺比對,**不得擴散到 `style-3-soc/`**。
   (0806 已定案不採用 Tailwind,該資料夾隨時可刪,刪掉這條缺口就消失。)
6. **`.trio`/`.quad`/`.duo` 的 hover 浮起是純視覺**,不代表可點——卡片本身不是連結,
   要點的是卡內的 `.go`。這是刻意的:整張卡當連結會讓卡內的第二個連結無處可放。
7. **`ess.html` 的 `.steps` 編號寫在標題文字裡**(`01 · Data collection`)而非 `.n` span,
   與其他頁的 mono 灰字編號長得不同。原因是那串編號屬於既有文案,拆出來會讓軸 3 判定少一句。
   要統一得先改文案並 commit,讓軸 3 的基準前進。

SC 1.4.13 Dismissible 原本也在這份清單上,已於 2026-08-06 修掉:`<header>` 帶一個行內
`onkeydown`,按 Esc 把焦點交給 logo(不是 `blur()`——blur 會把焦點丟回 body,
下一次 Tab 從整份文件最上面重來)。這與 navbtn 的行內 onclick 同級,不新增 `<script>` 標籤。
**滑鼠 hover 路徑仍然只能靠移開指標**,這部分未解。
