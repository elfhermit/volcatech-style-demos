# Copilot 專案指示 — Volcatech 官網 Demo(勝出風格 style-3-soc)

一律以繁體中文回覆;程式碼與技術術語保留原文。完整規則見根目錄 `CLAUDE.md`,重點如下:

- 本專案為靜態官網 demo。**2026-07-31 內部評選已結束**:勝出組合 = Style 3(SOC Console
  深色色系)× 原版直落版型,色系凍結。**2026-08-05 會議又定案三件事**:①首頁收斂為兩案;
  ②選單改三層、第一層不可點、全站統一 Nav B;③內容頁改版(0806 定案走守規則的 inline CSS 版,已落地)。
- 現行維護對象是 `style-3-soc/` **二十頁**:
  **2 個首頁**(`index` 現行版對照組 / `index-v1-proof` V1 信任前置)、
  3 個總覽頁(`cloud`＝CI、`cybersecurity`＝CS、`services`＝MS)、
  7 個 Cloud 分類頁(`cloud-compute` / `cloud-storage` / `cloud-analytics` /
  `cloud-serverless` / `cloud-databases` / `cloud-ai` / `cloud-services`＝CI-01〜CI-07)、
  **19 個 GCP 產品頁**(`gcp-*.html`,選單第三層;`gcp-cloud-armor.html` 是孤兒頁)、
  4 個資安產品頁(`sentinelone` / `threatsonar` / `cybereyes` / `google-secops`)
  與 1 個方案頁(`ess.html`)。根 `index.html` 是 Demo hub。
- **不要手改的檔案**:`index-v1-proof.html` 由 `docs/reports/build_v1_20260806.py` 產生;
  19 個 `gcp-*.html` 由 `build_gcp_pages_20260806.py` 產生;
  分類頁的雙出口連結與 `cloud.html#products` 索引由 `link_products_20260806.py` 產生;
  `lab/inline-cloud-compute.html` 由 `build_lab_20260806.py` 產生。要改就改腳本後重跑。
  **全站 header 由 `rebuild_nav_20260806.py` 產生,任何頁面的 `<header>` 都不要手寫。**
- **內容頁區塊元件(0806)**:`.probs`/`.uses`(琥珀左邊界)、`.trio`/`.quad`/`.duo`(icon 卡)、
  `.steps`(**只用於真的有先後順序**的流程,帶真箭頭)、`.spec`(深色編號面板)、`.stack`(分層圖)。
  **CSS 與 35 個 icon 的唯一正本是 `docs/reports/restyle_content_20260806.py`**——改元件樣式
  = 改 `BLOCK_CSS` 後重跑,36 檔一次同步;手改單頁 CSS 會讓 `check_nav` 立刻紅。
  **不得新增色票**(色系 0731 凍結),不得自繪新 icon 或引外部 icon 套件。
- **改內容頁版型時文案逐字不得變動**,跑 `python3 docs/reports/check_copy_20260806.py` 把關
  (拿 git 基準逐句比對 `<main>`;只放行 `.go` 標籤、箭頭、兩位數編號三類新增)。
- **`lab/` 是改版提案區(0806 新增,同日定案不採用 Tailwind),不是正式頁面**。其中兩個 Tailwind 頁**刻意違反**
  禁外部 CDN、禁框架、色系凍結三條硬性規則,用來讓「照會議 prompt 做的代價」被看見。
  **絕不可擴散到 `style-3-soc/`**;做法已搬回 `style-3-soc/`,該資料夾隨時可刪。
- **`archive/` 是已凍結的評選歷史**(落選風格、版型變體、舊總覽,以及 0805 封存的
  `style-3-homepage-variants/` 6 個首頁變體檔):**一律不修改、不 review、不納入任何檢查**。
  其中 `archive/Volcatech_Layout_Variants_GPT/` 是外部 AI 參考組,唯讀;
  它自帶的 `CLAUDE.md` / `README.md` / `HANDOVER.md` 只描述它自己,**不適用本專案**,
  規則衝突時一律以根目錄 `CLAUDE.md` 為準。
- **一致性鐵則是雙軸**(軸 1 已於 2026-08-06 換人):
  **軸 1** = 全站 36 檔的 `<header>` 與三段 nav CSS,正規化掉 5 個逐檔參數後**逐字節相同**
  (`python3 docs/reports/check_nav_20260806.py` 必須 PASS)。
  舊的「Nav A ↔ Nav B 自 `<main>` 起逐字節相同」隨 Nav A 退場而失效。
  **軸 2** = 兩個首頁凍結共用文案——H1、副標、Why H2、CTA 橫幅 H2、footer 品牌句這五句
  各命中 2 次;核心句 `We operate what we sell, and we build what we cannot buy.` 只在 V1
  出現(1 次),`index.html` 是**未經內容改動的對照組**,不得為了湊一致而改它。
- **選單是三層,第一層不可點**。唯一正本是 `rebuild_nav_20260806.py` 的 `MENU` 常數,不是任何 HTML:
  - 第一層 `Google Cloud` / `CyberSecurity` / `Services` 是
    `<button type="button" aria-haspopup="true">`,不是 `<a>`。用 button 而非 span
    是為了保留 keyboard focusable,`:focus-within` 才會生效、不需要 JS。
    button 的 CSS 重設**必須含 `padding:8px 0` 與 `line-height:inherit`**——
    `.menu a` 選不到 button,少了它面板會上移並在滑鼠移動時閃退。
    `.dd>a::after` 也必須寫成 `.dd>a::after,.dd>button::after`,否則下拉三角形全消失。
  - `Google Cloud` = Overview(`cloud.html`)＋六組 18 項,**18 項全部連各自的產品頁**。
  - `CyberSecurity` = Overview ＋ Endpoint — EDR / Detection — SIEM & WDR /
    Built in-house — Volcatech AI Security(只剩 CE-BAS)。
  - `Services`(扁平)= Overview ＋ ESS ＋ 24/7 SOC & IR ＋ GCP Managed Services。
  - **FortiEDR 與 GCP Managed Services 是不可點灰字**(`<span class="off">`＋mono 的
    Coming soon,用 `--muted` 上色)。**絕不可寫成 `<a href="#">`**——會踩到
    「每檔只能有 1 個 `href="#"`」的檢查。
  - `CyberSecurity` 駝峰是 0731 會議指定的**刻意寫法**,不要「修正」成 Cybersecurity
    (僅限選單分類名;H1 等內文仍為定稿原文)。
- **`aria-current` 與 `class="on"` 是兩個角色,不可混用**:`aria-current="page"` 掛
  「選單裡 href 等於本檔名的那個 `<a>`」(通常在第二層);第一層 button 的視覺高亮用
  非 ARIA 的 `class="on"`。⚠ 第一層從 `<a>` 換成 `<button>` 時,`.menu a[aria-current]`
  會匹配不到,**黃底線會靜默消失而 `grep -c` 仍回報正常**。
  選單裡沒有連結指向的頁面(目前只有 `cloud-services.html`)必須**明文登記**在
  `check_nav_20260806.py` 的 `ORPHANS`。
- **0805 從選單移除、但頁面區塊全部保留的項目**(只動選單是使用者明確裁決,不要「順手清乾淨」):
  AI-PTaaS、SecPurple、ISMS / PIMS、Penetration Testing、Cloud FinOps、Digital Transformation,
  以及更早移除的 Edge security(Cloud Armor)與 Volcatech cloud services 3 項。
  ⚠ 首頁 **Built by Volcatech 仍須列 CE-BAS / AI-PTaaS / SecPurple 三品**(硬性規則)。
- **選單 CSS 的三個坑,勿「順手統一」**:①`.dd ul` **絕不可加 overflow**(會變成 clip
  container 裁掉二層 flyout);②`.sub` 的四條規則一律 scope 成 `.menu .sub`(footer 有內文用的
  `<p class="sub">`);③901–1100px 這一段,二層改成在面板內就地展開(`position:static`),
  不是側開 flyout——該區間視窗放不下側開的 flyout,窄端會跑出左緣。
- **分層圖(`.stack`)的三條硬約束**:①不得用 `position:absolute`(768/390px 會崩,層間箭頭
  走 normal flow);②承載語意的線條用 `--muted` 不用 `--line`——`--line #27344A` 在
  `--bg #0E141F` 上只有 **1.47:1**,不到 WCAG 1.4.11 的 3:1;③箭頭用帶 `aria-hidden="true"`
  的真字元,不放進 `::before content`,也不用 `role="img"` 包整張圖(會把裡面的連結對輔助科技隱藏)。
  圖層標題不能單獨叫 `Operations` / `Platform`——會誤觸「舊選單術語不得殘留」的檢查。
- **GCP 產品頁不複製 `sentinelone.html`**:那個模板需要「成效 3 組＋沃凱交付 4 卡」,
  而 GCP 產品的沃凱觀點目前無素材。骨架(0806 三輪後)是 Hero →`#pain` 痛點(`probs`)→
  `trio` 3 卡 →`spec` 深色面板(尾列為帶來源註記的規格事實)→`uses` 琥珀左邊界 →
  `#pick` 選型指引 →`stack` 分層圖 →`#faq` 平鋪問答 → CTA。**不做頁籤**——全部平鋪成 section,
  可深連結、Ctrl+F 找得到。痛點/選型/FAQ 的素材取自 Google docs overview 頁改寫。
  `cards2` 必須偶數張(產品數為奇數時把清單改走 `loglist`)。
- **動 nav = 改 MENU 後重跑腳本**(36 檔一次同步);**動 footer = 36 檔都要改**
  (footer 沒有產生器,靠「17 個內容頁與 `sentinelone.html` 逐字節相同」把關)。
  頁尾三個欄標題都是連到對應總覽頁的連結。改完跑
  `check_nav_20260806.py`、`check_copy_20260806.py` 與 `check_links_20260806.py`,三支都要 PASS。
- 全 36 檔的 `main [id]` 都有 `scroll-margin-top:80px`,新增頁面要一併帶上;
  19 個 GCP 產品頁另需 `.stack a{scroll-margin-top:80px}`。
- `ess.html` 是方案頁:ESS(Enterprise Security Service)為沃凱打包方案
  (CyberEyes WDR + 多品牌 EDR + 自有 7x24 SOC),**方案層、非 19 項 SKU**;
  **全頁禁任何外部連結**。此規則只適用 `ess.html` 與 `services.html`——
  `cloud-services.html` 有 1 條指向 Cloud Armor 官方頁的外部連結(合法)。
- **已知待補項,不要自行編內容補上**:`cloud-services.html` 的沃凱自有服務 3 項
  (Cloud Migration & Kubernetes / Hybrid Cloud & Backup / Data & AI Engineering);
  `services.html` 的 5 項服務;`cybersecurity.html` 的 FortiEDR 描述;
  以及全站的合作夥伴等級、ISO 27001、EU region、交付模式、SLA 回應時間。
  ⚠ **紅線**:「Google SecOps 認證經銷商 / Cloud Security MSSP / Premier Partner」
  是**蓋亞(另一家公司)的資格**,寫成沃凱的等於不實陳述(見 `docs/product/google-secops.md`)。
- **SKU 代碼體系**:唯一事實來源 §A 的 `C-01`〜`C-06` 等是 **pre-0731 歷史體系**,
  保留封存、不對齊、不上站;現行 Cloud 線用頁面層代碼 `CI` / `CI-01`〜`CI-07`。
  GCP 產品頁沿用**父分類的代碼**(例 Compute Engine 是 `CI-01 · COMPUTE · COMPUTE ENGINE`),
  不新編 SKU 序號。
- **文案來源**:GCP 產品事實出自 `docs/GCP_Introduce.md` 與 `docs/GCP_Introduce_v2.md`;
  0806 三輪新增的痛點/選型/FAQ 取自 Google docs overview 頁改寫。
  改寫三原則:英式拼寫(-ise)、**刪原廠行銷倍數宣稱**(「快 4 倍」之類)、
  刪 `autonomous` / `AI-ready` / `unified` 這類自我定位形容詞。原廠描述必須改寫,不得複製。
  **金額一律不上站**(ADR 0004):單價/免費額度/促銷不寫,計價問題導向 Contact us;
  非金額的可查證規格事實(SLA 百分比、容量上限)可寫,來源 URL 註記在 `PAGES` 條目旁。
- 純靜態、單檔自足:HTML + inline CSS,禁止外部 CDN(含 Google Fonts)、禁止框架與建置步驟。
  **不得新增 `<script>` 標籤**——全站僅有的 JS 是各頁 header 的兩個行內 handler
  (navbtn 的 `onclick`、`<header>` 的 `onkeydown`;後者是按 Esc 關閉下拉,補 WCAG SC 1.4.13)。
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
  混入;二十頁的 tokens 與共用區塊需同步修改。
- WCAG 2.2 AA、`:focus-visible`、`prefers-reduced-motion`、RWD(390/768/1024/1440)、每頁唯一 h1;
  非英文片段(如「繁中」、中文公司名)必須帶 `lang` 屬性。
  **本 demo 不宣稱完全符合 AA**——五項已知缺口明文登記在 `CLAUDE.md` §已知缺口
  (下拉面板邊框對比 1.47:1、`aria-expanded` 刻意不寫、螢幕閱讀器瀏覽模式讀不到下拉、
  `aria-haspopup` 是半真話、`lab/` 用外部 CDN)。不要把它們當成待修 bug 順手改掉。
- 文案為歐洲 B2B 直述語氣,禁 hype 形容詞(leading / best-in-class / cutting-edge)與
  絕對化承諾(every / all / 100%);禁正文 ALL CAPS(mono 微標籤不在此限);
  日期用 `30 Jul 2026` 或 ISO 8601、24 小時制、電話 +886 國際格式、不放 LINE。
