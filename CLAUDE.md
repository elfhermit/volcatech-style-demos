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

現行 `style-3-soc/` 共 **40 頁**:2 首頁 ＋ 3 總覽 ＋ 7 Cloud 分類 ＋ **5 資安產品**(0810 新增
`argushack.html`)＋ 1 方案(ESS)＋ **19 GCP 產品頁**(0806 補齊,選單第三層)
＋ **1 服務頁**(0813 新增 `managed-gcp.html`,見下方 0813 決議)
＋ **2 法務頁**(0814 新增 `privacy.html` / `imprint.html`,見下方 0814 決議)。

**2026-08-13(地轉雲線建頁)**——選單 Services 底下原本的灰字 `GCP Managed Services` 已建頁,
並更名為 **`GCP Migration & Managed Services`**(`managed-gcp.html`)。素材出自使用者提供的
`docs/地轉雲_GCP_網頁製作企劃書_V1.md`;**內容正本是 `docs/地轉雲線_內容規劃_20260813.md`**
(逐區塊英文定稿文案、互連表、以及「企劃書哪些部分沒做、為什麼」的對照表)。四輪 grilling 決議摘要:

1. **一頁通吃 migrate ＋ run**——企劃書講的是遷移全流程,而選單那格叫 managed services,
   兩者不同;裁決為一頁涵蓋整個生命週期,選單標籤跟著改名。
   `cloud-services.html` 的 `Cloud Migration & Kubernetes` 卡加一條 `.go` 指向本頁,重疊解消
   (**該卡內文的 `[TODO]` 刻意不填**——本輪素材授權只解禁新頁)。
2. **檔名 `managed-gcp.html`**,刻意不用 `gcp-` 前綴——`gcp-*.html` 在本專案是「Google 產品頁」
   的保留語意,借用它會讓四條驗證指令(`#pain`/`#pick`/`#faq` 各須 1、`#stack` 須恰一個
   `.node.self`、`.stack a{scroll-margin-top}` 須 19 檔各 1、hero 晶片檢查)立刻紅。
3. **索引碼 `MS-01`**,為 Services 線建立 MS-NN 體例(CI/E/V 三線本來就有序號,只有 Services 沒有;
   `MS` 保留給總覽頁、`ESS` 是 programme 特例)。未來補的 SOC 頁是 `MS-02`。
4. **7 段骨架**:`#pain`(`.probs.four`,全站第一次用 `.four`)→ `#process`(`.steps` 六階段,
   **每階段只有一句**)→ `#services`(`.quad` 四卡,刻意與六階段錯開節奏)→ `#stack`(五層,
   頂層是沃凱自我節點)→ `#pick`(4 列,照全站慣例)→ `#plans`(`.trio` 三方案等重)→ `#faq`(6 題)。
   **`.fact` 豁免**(比照 `ess.html`,服務頁非產品頁),故 `.fact` 仍是 24 頁。
5. **24/7 沿用**但口徑限定為**監控與告警**;回應時間目標與 SLA 是本頁唯一的
   `[TODO: response time targets]`。企劃書自己禁「未經確認前寫入 24×7 與特定 SLA」,
   前半由使用者裁決解禁(站上 `services.html` 早有 24/7 SOC 宣稱),後半維持。
6. **這頁是手維護頁**(比照 6 個資安產品頁),沒有產生器;header 與四段 CSS 仍由
   `rebuild_nav` / `restyle_content` 統一,不得手改。

**2026-08-14(客戶 demo 前整備)**——起點是使用者一句話:「這週末要 demo 給客戶,
先把不確定的資訊(例如 TODO)移除,移到待處理清單讓我後續補齊,先讓網站看起來像個成品。」
四輪 grilling 定案。**待補清單正本= `docs/待補素材清單_20260814.md`**(由
`build_todo_backlog_20260814.py` 產生,不要手改)。決議摘要:

1. **384 處 `[TODO]` 裡 79% 是頁尾法定欄位**,使用者當場提供後一次解掉約 304 處。
   剩餘 80 處的內容型佔位符分三種處置:**能寫實話的寫實話**(11 張服務卡)、
   **要看合約才知道的改成「按案議定」**(約 30 處,不含數字與 SLA 故不構成承諾)、
   **事實不能編的刪句或改 `available on request`**(認證、夥伴等級、客戶案例、原廠法人名)。
2. **站上 `[TODO]` 歸零**,唯一例外是 `index-v1-proof.html` 的 10 處
   ——使用者裁決 V1 先不動,而它 0814 起已無任何入口連結,客戶動線走不到。
   ⚠ 首頁若定案選 V1,這 10 處要先清掉。
3. **新增兩個法務頁** `privacy.html` / `imprint.html`(`build_legal_pages_20260814.py`,
   **不得手改**)。理由:歐洲企業買家會主動去頁尾找隱私政策與 Impressum,找不到本身就是異常訊號;
   而這個站的隱私政策是最容易寫實話的一種(零 cookie、零第三方請求、零分析、零表單)。
   **不新增任何 CSS**——版面只用既有元件,加一條新規則就會讓軸 1 紅。
4. **清掉三處「這是 demo」的自白**:①38 頁頁尾的 `Demo notice: this page is published for
   internal design review only… The company details above are placeholders`
   (改寫成只保留「零 cookie、零第三方資源」那句真話);②38 頁底部的 backlink 導覽列;
   ③點不動的語言切換。
5. **FortiEDR 下架**(選單、`cybersecurity.html` 的卡片、全站頁尾那列、V1 的夥伴卡與服務索引)。
   理由:同組另兩個 EDR 都點得進去,只有它點不動——那讀起來是「還沒談成」而不是「即將推出」。
   EDR 組因此由 `.trio` 改 `.duo`(比照 detection 組的 2 卡慣例)。
6. **`lab/` 與 `archive/` 維持線上**(使用者裁決)。移除 backlink 列之後,
   客戶只有手動改網址才到得了根 hub 與這兩區。
7. **頁尾 `.legal` 灰字帶整塊移除**(當日稍晚追加,使用者指示「先移除」)——法人名／登記地址／
   統編／法務頁連結／©／「零 cookie」那句。頁尾仍保留聯絡 `<dl>`(Email／電話／登記地址)
   與 Company 欄的 `Privacy notice` / `Imprint` 兩條連結,法務頁入口沒有斷;
   法定身分資料集中在 `imprint.html`。做法與復原開關見
   `fix_footer_20260814.py` 的 ⑥ 與 `RESTORE_LEGAL`。
   ⚠ 連帶影響:V1 的 `.legalrow` 原本指 `#legal` 錨點,已改指兩個實頁
   (`build_v1_20260806.py`,是 check_links 逼出來的必要改動)。
8. **Contact 動線接上信箱**(當日稍晚追加)。盤點三個鏡頭各自獨立抓到同一件事:全站 118 個
   `Contact us`、132 顆 CTA 按鈕,而終點那顆是 `<a class="btn" href="#contact">` 掛在
   `<div class="band" id="contact">` 裡面——**點下去畫面不動**;頁尾 Email 與電話是不能點的純文字。
   使用者裁決:**不做 contact 頁,直接接 `mailto:`**。做法見 `wire_contact_20260814.py`:
   132 顆按鈕改 mailto(主旨帶該頁 h1,`Request a demo` 用 `Demo request:` 前綴以資區別),
   頁尾 Email/Phone 包成 `mailto:`/`tel:`。
   ⚠ header 與頁尾 Company 欄的 `Contact` **維持指向 `index.html#contact`**——那一區的 H2
   本身是有內容的,而且要讓 `#contact` 錨點保持有人引用。
   ⚠ **公司信箱同時由 `info@` 改為 `salesgroup@volcatech.com`**(使用者提供)。
9. **0814 盤點抓到的其餘修正**(來源 `docs/reports/改善盤點_20260814.md`,51 條成立發現):
   `index.html` 與 V1 的 `This demo loads…` 改 `This site loads…`(**站上最後一句 demo 自白**)、
   `cybersecurity.html` 的 `Three endpoint platforms` 改 `Two`(FortiEDR 下架後只剩兩張卡)、
   `.lead` 補進 `BLOCK_CSS`(24 頁在用、只有 2 頁定義過,其餘 22 頁行長拉到 152–166 字元)、
   `managed-gcp.html` 六階段流程圖改用 `.steps.six`(原本排不成一列,第 6 格獨自換行、
   前面那個箭頭指向空白)、`All ai services` → `All AI services`、`imprint` 版權行的 `Ltd..`、
   `ess.html` 三處美式拼寫、V1 服務目錄補上 `managed-gcp`(6→7 services)。
   ⚠ **Fortinet 維持在夥伴清單**(使用者裁決:是真夥伴,只是產品頁素材未到)——
   所以只改標題數字,不動 `index.html` 的 vendors 列與 `cybersecurity.html` 的 vendor 行。

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

**2026-08-06 第三輪(產品頁吸引閱讀改版)**又定案五件事(grilling 兩輪問答;研究底稿
`docs/reports/gcp官網解剖_20260806.md`——抽樣 5 個 Google 官網產品頁的結論:
吸引企業買家的是「決策支援」內容,不是規格):

1. **19 個 GCP 產品頁各加三段**:`#pain`(痛點,用 `probs`)、`#pick`(選型指引,新元件)、
   `#faq`(平鋪問答,新元件)。素材取自 Google docs overview 頁改寫,每組草稿都過
   獨立稽核(抄襲 6 連詞比對/虛構/金額/英式拼寫)。**競品座標句不做**——
   不與 AWS/Azure 等他雲比較,比較只限 19 個產品之間。
2. **全站不放金額資訊**(ADR 0004):單價、免費額度、促銷一律不寫,
   計價問題一律導向 Contact us。
3. **數字邊界放寬,僅限非金額**:可查證的規格事實(SLA 百分比、容量上限)可寫,
   放在 `spec` 面板;每個數字的來源 URL 以 `# src:` 註解記在
   `build_gcp_pages_20260806.py` 的 `PAGES` 條目旁,不渲染上頁。
4. **icon 規則放寬**:優先從 `ICONS` 挑,不夠用時以同風格自繪補進正本再用;
   區塊級 SVG 示意圖已授權但本輪未用到。
5. 適用面只動 `gcp-*` 19 頁;`.pick`/`.faq` 是通用元件——**資安線已於 2026-08-07 跟進**
   (4 產品頁＋`ess.html` 各補 `#pick`/`#faq` 兩段,CSS 零改造;痛點段 0806 區塊化時已有)。

**2026-08-10(會議延期,會前指示)**:①`ess.html` 移除 `#coverage`(時間軸)與
`#scenarios`(場景)兩區(業務指示;`#pick`/`#faq` 保留);②根 hub 新增
「待做事項與產品清單」區(JS 排序破例見硬性規則 1;正本= `docs/reports/build_updates_20260810.py`);
③內容充實三線與其餘決議見 `docs/meeting_0810.md` 附錄。

**2026-08-10 第二輪(ArgusHack 重定位)**——決議 16–24,正本 `docs/meeting_0810.md` 附錄二;
查證底稿 `docs/reports/argushack_歸屬與功能研究_20260810.md`。起因是查證確認
**原 `CE-BAS` 的「沃凱自研」宣稱有誤**:該 BAS 平台的原廠是台灣**盧氪賽忒(Leukocyte-Lab)**,
沃凱是**代理商**(使用者已確認)。因此:

1. **產品更名 `ArgusHack`**(不是 CE-BAS,也不是曾提過的 BAS-ArgusHack),頁面標明
   原廠 by Leukocyte-Lab。
2. **升格獨立產品頁** `argushack.html`(骨架照資安產品頁,含 `#pain`/`#pick`/`#faq`)。
3. **選單 CyberSecurity 第三組由「Built in-house — Volcatech AI Security」改為
   `Validation — breach & attack simulation`**,指向 `cybersecurity.html#validation`,
   底下掛 ArgusHack。下拉 head 白話行同步改為 `CyberSecurity — EDR · SIEM & WDR · BAS`。
4. **首頁 Built by Volcatech 區改寫成「我們自己維運」定位**——不再宣稱自研,
   只放有產品頁的 ArgusHack(區塊 id `#built` 不變;`.cols3` 改 `.duo`)。
5. **`AI-PTaaS` 與 `SecPurple` 全站移除**(首頁、`cybersecurity.html` 區塊、全站頁尾清單、
   V1 的 catalogue 與網絡圖)。⚠ 理由是**素材不足,不是否定它們是自研**;
   素材到位後可加回(已列進 hub 的待做事項)。
6. **`index.html`「內容未經改動的對照組」前提正式終結**——本輪一次改到底、含兩個首頁。
   軸 2 的凍結清單仍然有效(那些句子本輪沒動),但「對照組不得為了湊一致而修改」的
   理由已不再成立,詳見〈軸 2〉。

**首頁兩案**

| 方案 | 檔名 | hero 之後第一眼 |
|---|---|---|
| 現行 | `index.html` | Built → Why → Trust → Vendors(六個純文字) |
| V1 信任前置 | `index-v1-proof.html` | **How we work** 三步驟 → Trust 四項(資料主權/存取控制) → Partners 六張能力卡 |

V1 **不得手改**——由 `docs/reports/build_v1_20260806.py` 從 `index.html` 切片產生
(共用區塊 hero / Built / Why / Trust / CTA 直接取自現行首頁,確保逐字節相同)。
V1 專屬區塊代號:`#how`(交付三步)、`#partners`(夥伴)、`#catalogue`(服務索引)。
核心句 `We operate what we sell, and we build what we cannot buy.` 只在 V1 出現
(**`index.html` 刻意不含**——0810 之前的理由是「它是未經內容改動的對照組」,那個前提已終結;
現在的理由是**這句話本身**:沃凱並非什麼都自建,ArgusHack 就是代理的,
兩案的差異點保留在 V1 才不會讓現行版跟著做出過強的宣稱)。
- **GCP 產品頁 19 頁**(2026-08-06 補齊,選單第三層):18 個 GCP 產品各一頁,
  ＋ `gcp-cloud-armor.html`(孤兒頁,見下)。由 `docs/reports/build_gcp_pages_20260806.py`
  以 `cloud-compute.html` 為底檔產生(head / tokens / header / footer 全部沿用,只換 `<main>`)。
  **骨架與資安產品頁不同**(0806 三輪後的現況):Hero → `#pain` 痛點(`probs`)→
  核心優勢 3 卡(`trio`,自繪 SVG icon)→關鍵特色(`spec` 深色面板＋mono 編號,
  尾列是帶來源註記的規格事實)→適用場景(`uses`,琥珀左邊界)→ `#pick` 選型指引(`.pick`)→
  Works with(`stack`＋`flowmark` 真箭頭)→ `#faq`(`.faq`)→ CTA。
  刻意**不含**「成效／沃凱交付 4 卡」——那兩區需要沃凱觀點素材,目前沒有;
  痛點段的素材是 Google docs overview 的工程觀點(0806 三輪),不是沃凱觀點,素材到位後可再校。
  **不做頁籤**(0805 決策):Key features 與 Use cases 平鋪成兩個 section,可深連結、Ctrl+F 找得到。
  檔名用 `gcp-` 前綴,避免與分類頁的 `cloud-*` 撞前綴、也避開錨點檢查的 `cloud*.html` glob。
  文案正本 `docs/GCP_Introduce_v2.md`(**19 個產品全部有素材**,每產品 7 欄位;
  舊版 CLAUDE.md 說「約 5 個產品素材太薄」已於 0806 實測推翻,唯一破格的是 Model Garden——
  它沒有「關鍵特色」欄,改為模型清單)。改寫三原則:英式拼寫、
  **刪原廠量化宣稱**(4x／11 個 9 之類)、刪 `autonomous`/`AI-ready`/`unified` 這類自我定位詞。
  每頁的 `stack` 都必須有一個**沒有 href 的自我節點**(渲染成 `.node.self`),否則圖裡看不出主角是誰。
  `stack` 的節點一律連 `gcp-*.html`,不再連「分類頁#錨點」。
- 資安產品頁:`sentinelone.html`、`threatsonar.html`、`cybereyes.html`、
  `google-secops.html`(2026-08-03 依 `docs/product/` 內部素材新建)＋
  **`argushack.html`(2026-08-10 新建**,BAS;原廠 Leukocyte-Lab,沃凱代理);
  另有方案頁 `ess.html`
  (ESS=沃凱打包方案 WDR+EDR+7x24 SOC,非 19 項 SKU;**全頁零外部連結**,入口在 Services 下拉)。
  2026-08-07 五頁各補 `#pick`(插於 `#why` 前)與 `#faq`(4 產品頁插於 vendor 區前、ess 插於
  CTA band 前);`argushack.html` 建頁時就帶 `#pain`/`#pick`/`#faq`。
  **這 6 頁是手維護頁**(非產生器產出),素材經產文＋獨立稽核兩道 agent 工序;
  選型互連軸:SentinelOne↔ThreatSonar(日常防護 vs 獵捕鑑識)、CyberEyes↔Google SecOps
  (託管 WDR vs 自建 SIEM)、單品↔ESS、**ArgusHack↔各防護產品(驗證 vs 防護)**。
  FAQ 內的 `[TODO]` 照 `gcp-vertex-ai.html:506` 先例
  用純文字不包 span,且一律指名缺什麼(禁「to be confirmed」這種同義反覆)。
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
- CyberSecurity:Overview ＋ Endpoint—EDR(SentinelOne / ThreatSonar;
  ⚠ **0814 起只有這兩項**——FortiEDR 因零素材下架)、
  Detection—SIEM & WDR(CyberEyes / Google SecOps)、
  **Validation—breach & attack simulation(ArgusHack → `argushack.html`)**。
  WDR 併記是因 CyberEyes 實為 WDR;第三組原為「Built in-house—Volcatech AI Security(CE-BAS)」,
  0810 查證確認非自研後改為能力分類(見上方 0810 第二輪)。
  下拉 head 白話行:`CyberSecurity — EDR · SIEM &amp; WDR · BAS`。
- Services(扁平,無第二層):Overview ＋ ESS ＋ 24/7 SOC & IR ＋
  **GCP Migration & Managed Services**(0813 建頁前是灰字,現為真連結 `managed-gcp.html`)。
- **灰字項**(`<span class="off">`,附 mono 的 Coming soon)= 尚無內頁的項目,刻意不可 focus。
  ⚠ **0814 起全站沒有任何灰字項**(FortiEDR 下架;`check_nav` 的 `class="off"` 期望值
  0805 是 2、0813 是 1、**現在是 0**)。要加回灰字項時用 `--muted` 上色
  (對 `--surface` 6.79:1,過 AA),**絕不可寫成 `<a href="#">`**——全站 `href="#"`
  0814 起應為 0,一寫這條檢查就紅。
- **語言切換(EN / 繁中)已於 0814 整組移除**。繁中原本是 `href="#"` 死連結,
  且 title 寫著「正式站上線時會發佈中文版」——一個點不動的語言選項比沒有更像半成品,
  那句提示更等於對訪客宣告眼前這個不是正式站。雙語留給正式 Astro 版;
  `.lang` 的 CSS 規則也一併從 `CSS_DESK` / `CSS_MOB` 刪除。
- 每個下拉第一行保留 mono 白話對照(`li.head`)。
- ⚠️ **`.dd ul` 絕不可加 overflow** —— 會變成 clip container 裁掉二層 flyout。
  Nav B 的第一層面板最多 8 列,不需要捲動(Nav A 時代的 `max-height`/`overflow-y` 已隨 Nav A 一起退場)。
- ⚠️ **`.sub` 的四條規則一律 scope 成 `.menu .sub`** —— footer 有內文用的 `<p class="sub">`。
- ⚠️ 901–1100px 這一段,二層改成**在面板內就地展開**(`position:static`),不是側開 flyout:
  該區間視窗放不下側開的 flyout,窄端會跑出左緣。

**0805 從選單移除的 4 項(只動選單,頁面區塊全部保留)**

Services 的 `ISMS / PIMS`、`Penetration Testing`、`Cloud FinOps`、`Digital Transformation`。
這四項在 `services.html` 的區塊與頁尾清單一律照舊,只是不出現在下拉裡。
同理 0805 移除的 `Edge security`(Cloud Armor)與 `Volcatech cloud services` 兩組——
`cloud-services.html` 頁面與頁尾那列都還在。

⚠ 0805 一併移出選單的 CyberSecurity 兩項 `AI-PTaaS`、`SecPurple` **已於 0810 全站移除**
(頁面區塊、頁尾清單、首頁 Built 區都不再有),不再屬於「只動選單」那一類——
理由是素材不足,不是否定它們是自研,素材到位後可加回。

評選期的 4 個色系風格(style-1/2/4)、4 個版型變體(layout-1〜4)、外部 AI 參考組,
以及 0805 封存的 6 個首頁變體檔(`archive/style-3-homepage-variants/`)
已全部**凍結封存於 `archive/`**(封存總覽= `archive/index.html`),一律不再修改;
根 `index.html` 是 Demo hub:首屏講本輪落地了什麼,下方依序為兩個首頁方案、兩個總覽頁、
style-3 全部內容頁、**lab/ 內容頁改版提案**、歷史存檔入口。
⚠ **0814 起全站沒有 backlink 列**:原本每一頁底部都有 `← Style home · Demo hub`
(兩個首頁那列還多了 `Layout: Current · V1`),它把客戶直接送進這個中文進度儀表板。
副作用是 **V1 現在沒有任何入口連結**——檔案保留,等首頁定案。

- 目標受眾:歐洲企業的 IT / 資安決策者;語言英文為主(正式版另有繁中 /zh-tw/,架構須可擴充更多語系)
  ⚠ **0814 使用者補充:這個站的第一線讀者是「歐洲的合作夥伴」**——他們要拿這個網站
  在當地銷售沃凱的服務。所以站上缺的不只是給終端買家的信任元素,還有給夥伴的東西:
  交付分工(誰做哪一段)、誰簽約誰開發票、以及夥伴一定會被客戶問到的
  「你們的 24/7 SOC 在哪裡、誰輪班、歐洲時區誰接」。目前全站文案是「我們賣給你」的口吻,
  **一處都沒有回答上述問題**。已列進根 hub 待做事項,尚未動工。
- 新官網將**改版取代**現有 volcatech.com
- 法定資訊(0814 使用者提供):法人名 `Volcatech Corporate Ltd.`
  (沃凱科技股份有限公司)、統編 `94269177`、
  英文地址 `9F.-2, No. 54, Songjiang Rd., Zhongshan Dist., Taipei City 104090, Taiwan (R.O.C.)`、
  電話 `+886 2 2327 9668`、Email `salesgroup@volcatech.com`。
  ⚠ **`VAT / tax ID` 那一列刻意整列刪除**:台灣公司沒有 EU VAT 號,統編就是稅籍編號;
  填進 `VAT / tax ID` 會讓歐洲買家拿去 VIES 查而查不到,那是實質誤導。
  現在寫成 `Company registration no. (Taiwan): 94269177`,把管轄標在欄位名裡。
  ⚠ **0814 稍晚:頁尾最底那條 `.legal` 灰字帶(法人名／登記地址／統編／©／零 cookie 那句)
  已整塊移除**(使用者指示「先移除」),做法在 `fix_footer_20260814.py` 的 ⑥。
  現況是:**Email／電話／登記地址**仍在 40 檔頁尾的聯絡 `<dl>` 裡;
  **法人名與統編只剩 `imprint.html` 一處**(那正是 Impressum 頁的用途),
  入口是頁尾 Company 欄的 `Privacy notice` / `Imprint` 兩條連結,沒有斷。
  要復原把該腳本的 `RESTORE_LEGAL` 改 `True` 跑一次即可
  (`.legal` 的 6 行 CSS 刻意留在各頁 `<head>`,就是為了讓復原不必再碰 CSS)。
- 公司事實可信來源:`docs/公司_104.md`(僅可用於服務範圍與願景,**永遠不可**用來填統編/VAT/地址
  ——它是公司自述,不是法定登記資料)。
  ⚠️ 2026-08-04 使用者指示先不參考它,0806 再次確認維持。
  ⚠️ **0813 局部解禁**:`docs/地轉雲_GCP_網頁製作企劃書_V1.md` 只解禁 `managed-gcp.html` 一頁。
  ⚠️ **0814 局部解禁**:`公司_104.md` 解禁,**僅限服務範圍描述**,用來補寫 11 張只有佔位符的
  服務卡(`services.html` 5 張、`cloud.html` 與 `cloud-services.html` 各 3 張)。
  這條**取代**了 0813「`cloud-services.html` 那三張卡的 `[TODO]` 一律不動」的限制。
  法定資訊仍然一律不得取自該檔。
- 下一步:①**兩個首頁二選一**(現行版 vs V1;0814 起 V1 已無入口連結,客戶動線只走現行版);
  ②**取得認證與夥伴身分的證明**——ISO 27001 認證狀態/範圍/證書號、Google Cloud 夥伴身分與等級、
  可對外引用的客戶案例。站上這些位置 0814 起寫 `available on request` 或整句不寫,
  **未經確認絕不可填**;
  ③**把「按案議定」換成具體 SLA**——約 30 處交付分工與回應時間 0814 已從佔位符改成
  不含承諾的敘述,素材到位可換成實數;
  ④補齊 Services 線其餘服務頁(0813 已補 `managed-gcp.html`,尚缺 SOC 獨立頁與 0805 移出選單的四項);
  ⑤**FortiEDR 素材**(0814 因零素材下架,加回流程見待補清單);
  ⑥**視覺方向 A/B 裁決**(0812 新增,`lab/restyle-0812/`——採 A、採 B、A＋B 挑幾條、或都不採;
  比對頁附六項判準表。B 的「表面加深」需先依 ADR 0005 解凍,字級收斂不需要);
  ⑦再依 `docs/Volcatech_多風格_Build_Prompts.md` 的「共用基底 + 勝出風格模組」
  產生正式 **Astro** 版(雙語 i18n、GDPR 隱私頁、sitemap/hreflang)
  ~~決定其餘 15 個 GCP 產品頁做不做~~、~~cloud.html 要不要展開成產品層~~ 已於 0806 完成。
- **唯一事實來源(SSOT)**:`docs/Volcatech_多風格_Build_Prompts.md`(§A 19 項服務清單已於 2026-08-04
  定案為 **pre-0731 歷史體系**——保留封存、不改內容、新架構不對齊它;
  §B style-3 模組的選單逐字定義同為**評選期歷史**,選單分類以本檔上述 0731 決議為準)。
  Cloud 線的內容正本是 `docs/Cloud線_內容規劃_20260804.md`,不是 SSOT §A;
  `managed-gcp.html` 的內容正本是 `docs/地轉雲線_內容規劃_20260813.md`(來源素材
  `docs/地轉雲_GCP_網頁製作企劃書_V1.md`)。
  `docs/官網建置計畫_Build_Prompt_v3.md` 已凍結為 **legacy**(僅供背景脈絡,勿照做)。

## 硬性規則(所有修改必須遵守)

1. **純靜態、單檔自足**:demo 頁為 HTML + inline CSS(+極少量原生 JS,僅限手機選單/下拉);
   禁止外部 CDN(含 Google Fonts,GDPR)、禁止前端框架、禁止建置步驟。
   ⚠ **0814 唯一例外:`<link rel="icon" href="favicon.png">`**(同源相對路徑、零第三方請求)。
   GitHub Pages 是子路徑部署,瀏覽器預設要的 `/favicon.ico` 在網域根目錄不歸我們管,
   沒有這一行就沒有分頁圖示,沒有繞過的辦法。正本 `build_favicon_20260814.py`。
   2026-08-10 破例:專案根 Demo hub(根 index.html)的「待做事項與產品清單」區允許
   約 15–20 行行內原生 JS 做表格排序;破例僅限 hub 一頁,style-3-soc/ 各頁仍禁止新增 script。
2. **相對路徑**:所有連結與資源用相對路徑(需相容 GitHub Pages 子路徑 `/repo名稱/`)。
3. **首屏鐵則**:首頁首屏必須有 H1 一句話 + 明列**三條業務板塊**
   (Cloud Infrastructure / Cybersecurity / Managed Services)各附入口連結。
   任何改版不得破壞「3 秒看懂賣什麼(雲端 + 資安 + 託管維運)」。
   - H1 定稿(不得改寫):
     `Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`
   - 副標定稿:`We design and run Google Cloud environments for European organisations, deploy and tune
     EDR and SIEM, and keep both under 24/7 monitoring. One team, one contract, one point of accountability.`
   - hero 文案(status 行 / H1 / 副標 / CTA)為**置中**呈現(0731 決議),下方 console 卡片維持靠左。
   - 首頁必備第 4 區(區塊 id 仍是 `#built`):**「我們自己維運」的安全驗證定位**——
     現行標題 `Tooling we operate, and evidence that it works.`,內容是 ArgusHack
     (BAS,原廠 Leukocyte-Lab)＋沃凱自己跑驗證演練這件事。
     它是首頁區塊,**不是**第 4 條產品線,**不進頂層導覽**。
     ⚠ **2026-08-10 變更**:本條原文為「首頁必備第 4 區 **Built by Volcatech**
     (自研 CE-BAS / AI-PTaaS / SecPurple)」。查證確認 CE-BAS 的原廠是盧氪賽忒
     (Leukocyte-Lab)、沃凱只是**代理商**,「自研」宣稱不成立(牴觸硬性規則 4 不虛構公司事實),
     故本條由使用者裁決改寫;AI-PTaaS / SecPurple 因素材不足一併移除(非否定其自研)。
     **這一區從此不得再宣稱「self-developed / built in-house / not resold」**,
     除非拿到經查證的自研產品素材。
4. **不虛構公司事實**:統編、地址、認證(ISO 等)、客戶案例、合作等級**未經確認一律不寫**。
   ⚠ **0814 起做法改了**:`[TODO: 說明]` 佔位符**不再出現在上站頁面**——客戶會看到它。
   改成三選一:**(a) 能寫實話就寫實話**;**(b) 要看合約才知道的,寫成不含數字與 SLA 的
   「按案議定」敘述**(例:`Delivery scope and response times are agreed per engagement.`);
   **(c) 事實不能編的,刪句或寫 `available on request`**。三者都不構成虛構宣稱。
   缺什麼一律登記進 `docs/待補素材清單_20260814.md`,**不要留在頁面上**。
   施工中的暫時佔位仍用 `[TODO: 說明]` 一種語法(不得用 `{{TODO}}`),但**不得 commit 上站**;
   建置參數用 `[VAR: 名稱]`。
5. **現行頁面只有 `style-3-soc/`**(design tokens 在各頁 `:root`);`archive/` 內所有頁面
   一律凍結不動——發現其中的問題只回報,不動手(理由見下方 archive 專節)。
6. **無障礙與品質**:WCAG 2.2 AA 對比、`:focus-visible`、`prefers-reduced-motion`、
   語意化 HTML、每頁唯一 `<h1>`、RWD(390 / 768 / 1024 / 1440px、無水平捲軸)。
7. **文案**:歐洲 B2B 直述語氣(做什麼、給誰、成果),禁「最先進/領導品牌」等 hype;
   日期用 `30 Jul 2026` 或 ISO 8601、24 小時制、電話 +886 國際格式、不放 LINE。
   **全站不放金額資訊**(單價/免費額度/促銷;ADR 0004)——計價問題一律導向 Contact us;
   非金額的可查證規格事實(SLA 百分比、容量上限)可寫,來源 URL 註記在產生器 `PAGES` 條目旁。
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

### 內容頁區塊元件(2026-08-06,全站 40 頁共用)

0805 的意見是「每頁都是同一個 `loglist` 重複三四次,讀起來是一整欄沒分別的文字」。
現在每一段各有自己的處理,眼睛在讀字之前就分得出它是哪一類:

| class | 語意角色 | 長相 |
|---|---|---|
| `.probs` / `.uses` | 痛點(專案前的狀態)／場景(為了什麼情境) | `--surface` ＋ 3px 琥珀左邊界;四項時加 `.four` |
| `.trio` / `.quad` / `.duo` | 產品、服務、能力卡 | `--surface` 卡 ＋ 自繪 SVG icon ＋ 可選 `.go` 連結;3／4／2 欄 |
| `.steps` | **有先後順序**的流程 | `#111A26` 節點 ＋ `--muted` 邊框 ＋ 節點間的真箭頭 |
| `.spec` | 事實／規格／成效清單 | `#111A26` 深色面板 ＋ mono 兩位數編號。**已改為雙欄交錯矩陣**(`grid-template-columns:repeat(2,1fr)`,偶數格帶左分隔線),消除單欄長條直落;768px 退單欄 |
| `.stack`＋`.layer`＋`.node`＋`.flowmark` | 分層架構圖(目前只在 `gcp-*.html`) | 分層方塊 ＋ 真箭頭 |
| `.loglist` | 緊湊索引(目前只在 `cloud.html#products`) | 帶邊框的單欄列表 ＋ 狀態圓點 |
| `.goes` | 一張卡有兩個出口時的連結列 | 把兩個 `.go` 併成一列,不讓它們各佔一行 |
| `.pick` | 選型指引:「情境 → 建議產品」(0806 三輪;`gcp-*.html` ＋ 0807 起資安線 5 頁) | `--surface` 列 ＋ 真箭頭 ＋ `.node` 晶片(建議是本頁自己時用 `.node.self`) |
| `.faq` | 平鋪問答(0806 三輪;`gcp-*.html` ＋ 0807 起資安線 5 頁) | **0811 起雙欄卡片**(CSS `columns:2`＋`--surface` 卡):FAQ 曾佔全頁 36–44% 是最大文字牆,雙欄後牆高砍半;640px 退單欄。仍全展開、Ctrl+F 找得到,刻意不用 disclosure widget |
| `.fact` | **hero 代表事實列**(0811;產品頁 24 頁,`ess.html` 豁免) | mono 編號 ＋ 琥珀 `.node.self` 晶片(列標題)＋ 事實內文。內容是從該頁 `.spec` **搬上來**的既有一列(面板該列不再渲染、編號留空缺),不是新寫的句子 |

**唯一正本是 `docs/reports/restyle_content_20260806.py` 的 `BLOCK_CSS`**(含 35 個自繪 icon 的
`ICONS` 常數)。改元件樣式 = 改那個常數後重跑腳本,40 檔一次同步;**手改單頁的 CSS 會讓軸 1 立刻紅**。

**0811 版型改版**(決議 25–34,`docs/meeting_0810.md` 附錄三;施工正本
`docs/reports/版型改版規劃_20260811.md`、數據 `docs/reports/內容頁密度體檢_20260811.md`):
0810 決議 11 的「不做全站系統性重排」已由使用者正式重開(**字體仍留 Astro 正式版**)。
本輪動了四件事——`.faq` 雙欄、`.spec` 緊湊化、`.fact` 新元件、節奏收斂
(`.phero~section .wrap` 直向 padding 80→64px)。⚠ **節奏規則靠 `.phero~section` 把兩個首頁
排除在外**——首頁沒有 `.phero` 所以天然免疫;哪天首頁用上 `.phero`/`.faq`/`.spec`,這個免疫就失效。

四條硬約束:
1. **不得新增色票**——區分只靠三層表面深度(`--bg` / `--surface` / `#111A26`)、一道琥珀邊界、
   一列真箭頭。0731 的色系凍結仍然成立。
2. `.steps` **只能用在真的有先後順序的內容上**。四個並列項目硬插箭頭 = 假造推進關係,
   是這輪最容易犯的錯。判不出順序就用 `.quad`。
3. `stack` 的三條沿用 V3:①不得用 `position:absolute`(768/390px 會崩);②承載語意的線條用
   `--muted` 不用 `--line`(`--line` 對 `--bg` 只有 **1.47:1**,不到 1.4.11 的 3:1);
   ③箭頭用帶 `aria-hidden="true"` 的真字元,不放進 `::before content`。
4. icon **優先從 `ICONS` 挑**;不夠用時以同風格自繪**補進正本**再用(0806 三輪放寬),
   仍禁外部 icon 套件、禁 `<img>`;同一頁不得重複。
5. (0811)**抽象節奏元素只准是抽象的**。四個無圖頁(API Gateway／Datastore／Filestore／
   Model Garden)用 `build_gcp_pages_20260806.py` 的 `fig_motif()` 補視覺喘息:放大的該頁 icon
   ＋兩側點狀虛線,`aria-hidden`、**無 `<title>`、無 figcaption、無箭頭、不成流程**。
   它不是機制圖——0810 決議 16「誠實優先:沒機制可畫就不畫」仍然成立,想加說明文字就會撞軸 3。

hover 有 2px 浮起 ＋ 邊框變色(**不加陰影**,專案禁 glow),`prefers-reduced-motion` 下關閉。

## 一致性鐵則:三軸

⚠️ **舊軸 1(Nav A ↔ Nav B 自 `<main>` 起逐字節相同)已於 2026-08-06 退場**——首頁收斂為 2 檔、
全站統一 Nav B 之後,A/B 對照物理上不存在了。它曾是全站**唯一**能自動抓到「手改漏一檔」的檢查,
所以必須有東西接手,新軸 1 就是那個接手的東西。

### 軸 1|全站 header 同源:正規化後 40 檔逐字節相同

`python3 docs/reports/check_nav_20260806.py` → 必須 PASS。

它把每檔的 `<header>` 與**四段 CSS**(三段 nav ＋ 0806 的區塊元件)取出,
正規化掉 5 個本來就該逐檔不同的參數
(EN 自指 href、logo/Home 目標、About/Contact 的錨點前綴、`aria-current` 落點、`class="on"` 落點)
之後,要求 **40 檔逐字節相同**;另外檢查結構數量(`li.sub`=9、`li.head`=3、button=3、
`.off`=**0**(0814 FortiEDR 下架後全站無灰字)、`li.grp`=0)、`aria-current` 落點、Esc handler、以及 `.dd ul` 沒有 overflow。

- **`aria-current="page"` 掛「選單裡 href 等於本檔名的那個 `<a>`」**,通常在第二層。
  第一層是 button,`.menu a[...]` 選不到它——所以視覺上的「你在這個區塊」改用
  `class="on"`(非 ARIA)掛在 button 上。這兩個角色不可混用。
- **孤兒頁登記**:選單裡沒有任何連結指向它的頁面,header 內就沒有 `aria-current`。
  目前有四個:`cloud-services.html`(0805 兩組移出選單所致)、`gcp-cloud-armor.html`
  (0806 補齊產品頁時一併產出,但它所屬的 Edge security 那組已被移出選單),
  以及 0814 新建的 `privacy.html` 與 `imprint.html`(入口在頁尾,慣例上不進選單)。
  ⚠ 兩個法務頁還要登記在 `check_nav` 的 **`NOSECTION`**:它們不隸屬任何板塊,
  第一層 button 不該有 `class="on"`,硬塞一個板塊會說謊。
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

最後一句刻意只在 V1 出現。⚠ **2026-08-10 起理由換了一套**:
原本的理由是「`index.html` 是未經內容改動的對照組,代表今天線上的樣子」——
0810 的 ArgusHack 重定位一次改到底、含兩個首頁,那個前提已經終結,
不要再用「它是對照組」當作不改 `index.html` 的依據。
現在的理由是**這句話本身的真確性**:沃凱並非什麼都自建(ArgusHack 就是代理的),
這句自我定位放在 V1 當差異點可以,讓兩案都講就變成全站宣稱、與硬性規則 4 相牴觸。
前五句仍逐字凍結(本輪沒動到它們),改任一句都要兩案一起改。

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
  ⚠ 「完全相同」指的是**兩案彼此逐字節相同**(驗法:`diff <(awk '/<section id="top"/,/<\/section>/' index.html)
  <(awk '/<section id="top"/,/<\/section>/' index-v1-proof.html)` 應無輸出),
  **不是**「與 git 某個歷史版本相同」——hero 文案本身可以改,只要兩案一起改。
  0810 就改過一次:Cybersecurity 卡的 `plus three AI-driven testing services we build ourselves.`
  改為 `plus breach and attack simulation to check that they hold.`,因為那三項自研測試服務
  兩項已全站移除、剩下一項確認是代理品,原句留著就是硬性規則 4 禁止的虛構事實。
  改 hero 一律改 `index.html` 再重跑 `build_v1_20260806.py`,不要手改 V1。
- 改任何共用內容(hero、Built、Why、Trust、footer)→ 改 `index.html` 後
  **重跑 `docs/reports/build_v1_20260806.py`**,V1 會自動跟上。
- 動到 nav 項目 → 改 `rebuild_nav_20260806.py` 的 `MENU` 後重跑,**全站 40 檔一次同步**;
  動到 footer 清單 → 40 檔都要改(footer 目前沒有產生器,靠逐字節比對把關)。
  ⚠ 兩者都要**順手重跑 `build_lab_20260806.py`**——`lab/inline-cloud-compute.html` 的
  header/footer 是從 `cloud-compute.html` 取的,它在 `check_links` 掃描範圍內。
  該腳本**刻意把底檔的區塊元件 CSS 整段剝掉**(0810 加的,`lab/` 那一頁自帶一份提案版),
  否則每跑一次就把全站元件搬進這個「留檔備查」的檔案——不要把那段剝除邏輯拿掉。
  子頁的錨點連結帶 `index.html` 前綴、同資料夾頁面用相對檔名。

## 實驗區:`lab/`

⚠ **2026-08-12 起 `lab/` 重新啟用**,底下有兩個彼此獨立的議題,規則不同:

| 子區 | 狀態 | 說明 |
|---|---|---|
| `lab/*.html`(第一層四檔) | **已定案、留檔備查** | 0806 的「內容頁改版:inline vs Tailwind」對照,見下方專節。隨時可刪 |
| `lab/restyle-0812/`(五檔) | **待裁決** | 0812 的視覺方向 A/B 提案,見下方專節 |

`check_links_20260806.py` 的 `lab/` 掃描已於 0812 由 `glob` 改為 **`rglob`**——
原本只掃第一層,子資料夾會靜默逃過檢查而腳本照樣印 PASS。新增 `lab/` 子資料夾時
不需要再改腳本,但**不要把它改回 `glob`**。

### `lab/restyle-0812/` — 視覺方向 A/B 提案(2026-08-12,待裁決)

起點是 `docs/reports/refero_design風格範本調查_20260811.md`(15 個深色候選)。
使用者挑了 Supabase 與 Harness.io,經四輪 grilling 裁決為**吸收手法、微調現行**(不換皮)。
⚠ 那份報告第 6、95 行寫「現階段不會立即採用任何候選、視覺風格維持不動」——
**該註記已於 0812 由使用者正式重開**,以 `docs/design/README.md` 為準。

⚠ **第一版(只改色彩)已作廢**。它一條版型都沒動,使用者回饋「只感受到色彩有一點點差異」。
根因是自我設限「markup 凍結」,而那個理由不成立——`check_copy` 本來就在比對文字節點集合。
**第二版(0812 現行)照兩個參考站的實測版型做**,配色、字體、版型三者都換:

- **A(Supabase 向)= 一次攤開**。`#121212` ＋ 單一綠 `#3ECF8E`(琥珀完全退場)、
  Inter ＋ Source Code Pro。四個招牌:**分裂式標題**(`section>.wrap` 改 grid `1fr 1fr`
  ＋ `align-items:end`,標題左、說明右、底線對齊)、**髮絲線分節**(每段相同 padding、
  不換底色)、**漸層髮絲邊框**、**12 欄 bento**(6+3+3,icon 放大 158px 沉進卡片右下角)。
- **B(Harness 向)= 漸進揭露 ＋ 不對稱**。`#0A0A0A`(平替 `#070707`,禁純黑)
  ＋ 薄荷綠 `#70DCD3` ＋ 信號藍 `#0092E4`、Geist ＋ Geist Mono。五個招牌:
  **不對稱 55%/30%**(右側刻意留 15% 空白)、**每段一個世界**(各自底色與 padding、
  max-width 1200↔1440 跳)、**FAQ 零 JS `<details>` 手風琴**、
  **架構圖改橫向可捲卡片列**、圓角柔化。
- 兩套都把 19 個 `font-size` 值收斂成 8 級階梯(數值各自調)。
- 四個範例頁**由 `build_restyle_samples_20260812.py` 產生,不要手改**。
  基底 CSS 一字不動、override 疊在 `<style>` 尾端;**markup 只動一處**——
  B 套把 FAQ 的每一項換成 `<details>`(`h3` 留在 `<summary>` 內,標題階層沒掉)。
  A 套的 `<main>` 仍與正式頁逐字節相同。全檔另有 3 處刻意的導覽改寫:
  `<title>` 前綴、EN 自指、backlink 列。
- **字體自架在 `lab/restyle-0812/fonts/`**(4 個 woff2、211KB、皆 SIL OFL 1.1,
  授權見該資料夾 `LICENSES.md`)。這是本 repo 第一次放二進位資產;
  提案不採用的話連同整個資料夾刪掉即可。**仍然零外部請求、零 `<script>`**。
- ⚠ B 套的 FAQ 手風琴**重開了 0805「不做頁籤」的決議**,但只重開 FAQ 這一段。
  代價明文登記:收合的答案在部分瀏覽器 Ctrl+F 找不到——那正是與 A 套的核心對照點。
- 設計文件在 **`docs/design/`**(不進版控):基線／A 規格／B 規格／落地路線圖。
  「色系凍結」的範圍定義在 **`docs/adr/0005-colour-freeze-scope.md`**。
- 選定後**不是把範例頁搬過去**,而是照 `docs/design/90_落地路線圖_20260812.md` 把每條改動
  併回 `restyle_content_20260806.py` 的 `BLOCK_CSS` 與各頁基底 CSS。

### `lab/` 第一層 — 內容頁改版比對(2026-08-06,已定案)

2026-08-06 新增,同日定案。**結果:選 inline CSS 版**,元件已搬進 `style-3-soc/` 全部 40 頁
(正本 `docs/reports/restyle_content_20260806.py`)。這四個檔自此只剩紀錄價值——
它保存了「當初為什麼沒選 Tailwind」的實際對照,**隨時可整個刪掉**,刪除時機由專案負責人決定
(刪的是這四個檔,不是整個 `lab/`——`restyle-0812/` 還在用)。
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
  0806 三輪起每筆條目還要含 `pains`/`picks`/`faqs` 欄位(格式照現有條目);
  規格數字必附 `# src:` 來源註解,金額一律不寫(ADR 0004)。
  0811 起還要挑一筆 `hero_fact`(1-based,指 `spec`＋`extra_specs` 合併清單的第 k 列)——
  **挑該頁獨有、內文 ≤26 詞的那列**;⚠ 別挑 `Availability commitment`(它出現在 17 頁,
  挑它會讓一票頁的 hero 長一樣,正好毀掉這個欄位存在的理由)。
  沒有機制可畫的頁再加 `"figures": {"features": fig_motif(ICONS["<未用過的 icon>"])}`。
- **補資安產品頁**:複製 `style-3-soc/sentinelone.html` → 改 `<title>`、meta description、
  eyebrow 索引碼、內容區塊;素材見 `docs/product/`(內部,先讀產品簡介總覽.md)。
  完成後跑 `rebuild_nav_20260806.py`(header 自動處理),並把 `MENU` 裡該項改成真連結。
  ⚠ `cards2` 必須偶數張(產品數為奇數時,把產品清單改走 `loglist`,`cards2` 留給沃凱交付項)。
- **補 Services 線服務頁**:骨架照 `managed-gcp.html`(0813)或 `ess.html`;索引碼走 **MS-NN** 序列
  (下一個是 `MS-02`)。**服務頁 `.fact` 一律豁免**——它是產品頁的元件,`.fact` 檔數維持 24。
  新頁完成後:①`rebuild_nav_20260806.py` 的 `MENU` 加真連結並重跑;②`services.html` 的
  `#catalogue` 加一張卡並帶 `id`(驗證指令的錨點清單要同步);③全站 footer 加一列
  (**footer 沒有產生器**,用「只在 `<footer>` 區域內取代」的腳本改,寬鬆子字串會誤中 header 的選單項);
  ④`check_nav_20260806.py` 的 `EXPECT_FILES` 與 `restyle_content_20260806.py` 的 `EXPECT_FILES`
  兩處都要 +1(兩支腳本各自寫死頁數),`build_updates_20260810.py` 的產品數守衛也要跟著調;
  ⑤重跑 `build_lab` 與 `build_restyle_samples`(它們的
  header/footer 取自底檔);⑥`build_updates_20260810.py` 的 `NOTES` 加一筆(key 必須與選單同名)。
- **補 Cloud 分類頁**:內容正本是 `docs/Cloud線_內容規劃_20260804.md`(§4 骨架、§5 逐項英文文案、
  §6 逐頁大綱);產品事實一律出自 `docs/GCP_Introduce.md`。
  每個產品在名冊 `loglist` 佔一列且**必須帶 `id`**(nav 深連結的落點),
  新頁必含 `main [id]{scroll-margin-top:80px}`,否則 66px sticky header 會蓋住落點。
- **改內容頁的版型**:元件樣式改 `restyle_content_20260806.py` 的 `BLOCK_CSS` 後重跑
  (40 檔一次同步);某一頁的 markup 則直接改該檔的 `<main>`。改完必跑
  `check_copy_20260806.py` 確認沒有把文案一起改掉。
  ⚠️ `.steps` 只能用在真的有先後順序的內容;判不出順序就用 `.quad`,不要為了版型假造推進關係。
- **版面定稿後**:勝出方案的內容搬進 `index.html`(現行版位置),另一個移入 `archive/`;
  首頁收斂為 1 檔,一致性鐵則的軸 2 隨之退場,`build_v1_20260806.py` 一併退役。
- **產生正式 Astro 版**:不要改造本 demo;在新資料夾/新 repo 依
  `docs/Volcatech_多風格_Build_Prompts.md`(基底 + style-3 模組,選單以 0805 決議覆蓋)執行,
  完成後跑該檔【品質底線(驗收)】清單(**不是** v3 的 §9,那份已失效)。

### ⚠ 腳本的執行順序不是隨意的(0814 踩到)

`build_gcp_pages` / `build_legal_pages` / `build_v1` 都是**從底檔複製 header 再換 `<main>`**,
所以它們產出的頁面帶著**底檔的** `aria-current` 與 `class="on"` —— 對新頁而言那是錯的。
**這三支跑完必須接 `rebuild_nav_20260806.py`**,否則 `check_nav` 會紅(0814 一次錯 21 檔)。

安全的完整順序(要重跑就照這個跑,可重複執行):

```bash
python3 docs/reports/build_gcp_pages_20260806.py
python3 docs/reports/build_legal_pages_20260814.py
python3 docs/reports/build_v1_20260806.py
python3 docs/reports/link_products_20260806.py
python3 docs/reports/fix_content_todos_20260814.py
python3 docs/reports/fix_footer_20260814.py
python3 docs/reports/wire_contact_20260814.py   # ← 必須排在會重寫 <main> 的三支之後
python3 docs/reports/restyle_content_20260806.py
python3 docs/reports/rebuild_nav_20260806.py    # ← 一定要最後跑
python3 docs/reports/build_favicon_20260814.py  # ← 必須排在 lab 兩支之前:它只注入
                                                #   style-3-soc/ 與根 hub,lab 是從底檔複製的
python3 docs/reports/build_lab_20260806.py      # 取自底檔,故排在 nav/footer 之後
python3 docs/reports/build_restyle_samples_20260812.py
python3 docs/reports/build_updates_20260810.py
```

⚠ **驗「冪等」不要派給唯讀 agent 去跑這些腳本**——它們會寫檔,而且有先後相依。
正確做法是主對話自己 `cp -r style-3-soc <scratchpad>/snap` → 依上表跑完 → `diff -rq` 比對。

### `docs/reports/` 腳本現況(2026-08-06)

| 腳本 | 做什麼 |
|---|---|
| `rebuild_nav_20260806.py` | **選單唯一正本**。整段抽換 header ＋ 三段 nav CSS,可重複執行 |
| `restyle_content_20260806.py` | **區塊元件 CSS ＋ 35 個 icon 的唯一正本**。注入 40 檔,可重複執行 |
| `check_nav_20260806.py` | 軸 1 檢查:40 檔 header ＋ 四段 CSS 逐字節相同 ＋ 結構數量 ＋ 孤兒登記 |
| `check_copy_20260806.py` | 軸 3 檢查:對 git 基準逐句比對 `<main>`,文案零漂移 |
| `check_links_20260806.py` | 標籤配對、唯一 h1、id 不重複、相對連結與錨點有效。0812 起 `lab/` 改用 **`rglob`** 遞迴掃子資料夾（原本的 `glob` 只掃第一層，子資料夾會靜默逃過檢查） |
| `build_restyle_samples_20260812.py` | 產生 `lab/restyle-0812/` 的 4 個視覺方向範例頁（第二版：配色＋字體＋版型全換）。基底 CSS 不動、override 疊在 `<style>` 尾端；**markup 只動一處**——B 套把 FAQ 每一項轉成 `<details>`（`to_accordion()`）。A/B 兩套 CSS 的**唯一正本**。⚠ header/footer 取自底檔 —— **改完選單或頁尾要重跑** |
| `build_v1_20260806.py` | 從 `index.html` 產生 `index-v1-proof.html`(0804 那支改造而來) |
| `build_gcp_pages_20260806.py` | 產生 19 個 GCP 產品頁(以 `cloud-compute.html` 為底檔)。**產品文案的唯一正本**;0811 起含 `hero_fact` 欄位與 `fig_motif()` |
| `link_products_20260806.py` | 分類頁 19 張產品卡的雙出口連結 ＋ `cloud.html#products` 索引。可重複執行 |
| `build_updates_20260810.py` | 產生根 hub「待做事項與產品清單」區(日期取 git log;備注 dict 手維護,更新前須經 Shiro 確認)。可重複執行。⚠ 0814 修掉一個自 0813 起讓它 `IndexError` 跑不動的欄位位移(`MENU` 的 `sub` 子項從 `row[3]` 移到 `row[4]`) |
| `build_legal_pages_20260814.py` | 產生 `privacy.html` ＋ `imprint.html`(以 `sentinelone.html` 為底檔)。**法務頁唯一正本**,不得手改頁面。⚠ 刻意零新增 CSS |
| `fix_footer_20260814.py` | 頁尾法定資訊補實 ＋ 移除 Demo notice/backlink 列/FortiEDR 那列。**只在 `<footer>` 之後動手**。可重複執行 |
| `fix_content_todos_20260814.py` | `<main>` 內容型佔位符的處置對照表(按案議定/刪句/available on request/11 張服務卡補寫)。**待補清單的資料來源** |
| `wire_contact_20260814.py` | **Contact 動線正本**(0814 稍晚):132 顆 CTA 按鈕由 `#contact` 改 `mailto:`(主旨帶該頁 h1)＋頁尾 Email/Phone 包成 `mailto:`/`tel:`。⚠ 必須排在 `build_gcp_pages`／`build_v1`／`build_legal_pages` 之後——那三支會整段重寫 `<main>`,把按鈕還原 |
| `build_favicon_20260814.py` | **favicon 正本**(0814):從 `docs/assets/volcatech-logo-final.png` 裁出「A」火山字符 → 256×256 透明 PNG,並在 41 檔注入 `<link rel="icon">`。不依賴 Pillow(PNG 解/編碼都在檔內)。⚠ 母檔在 `docs/` 底下,不進版控;產出的 `favicon.png` 有進版控,所以站不會壞,但要重產得先把母檔放回去 |
| `build_todo_backlog_20260814.py` | 由上一支的對照表產生 `docs/待補素材清單_20260814.md`。改了對照表就重跑它 |
| `rename_argushack_footer_20260810.py` | 0810 全站 footer 更名(CE-BAS→ArgusHack、移除兩品那兩列)。可重複執行,只動 footer |
| `build_lab_20260806.py` | 產生 `lab/inline-cloud-compute.html`(**已完成階段任務**,`lab/` 刪掉後可一併移除)。⚠ 它從 `cloud-compute.html` 取 header/footer/CSS,所以**改完選單或頁尾要重跑它**——`lab/` 在 `check_links` 掃描範圍內,漏跑就會出現死錨點(0810 實際踩到) |
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
| **視覺設計文件**(現況基線、風格提案規格、可貼 AI 的 prompt、落地路線圖) | `docs/design/`(2026-08-12 建立);索引在其內 `README.md`。⚠ 它是**提案區不是正本**——tokens 正本仍是 CLAUDE.md 速查表 ＋ Build_Prompts §B ＋ 40 檔 `:root` |
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
python3 docs/reports/check_nav_20260806.py     # 軸 1:40 檔 header ＋ 四段 CSS 同源、結構數量、孤兒登記
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
# 核心句只在 V1 → 應輸出 1(index.html 刻意不含,理由見〈軸 2〉)
grep -Fl 'We operate what we sell, and we build what we cannot buy.' index*.html | wc -l
# 無外部資源請求 → 應為空(全站唯一 JS 是各頁 navbtn 的行內 onclick;不得新增 <script> 標籤)
# ⚠ 0814 起 `<link rel="icon" href="favicon.png">` 是**唯一合法的 `<link>`**:同源相對路徑、
#   零第三方請求,不違反 GDPR 前提。GitHub Pages 是子路徑部署,瀏覽器預設要的
#   `/favicon.ico` 落在網域根目錄(不歸我們管),所以沒有這一行就沒有分頁圖示。
#   其餘任何 `<link>`、`<img>`、`<script>`、`@import` 一律仍然禁止
grep -nE '<img |<script|@import|<link ' *.html | grep -v '<link rel="icon" href="favicon.png">'
# 外連只該是原廠 anchor,且同行有 rel="noopener" → 應為空
grep -n 'https\?://' *.html | grep -v 'rel="noopener"'
# CTA 一律 Contact us(sentence case);禁 Contact Us、禁 Request a proposal
grep -oh 'Contact us\|Contact Us\|Request a proposal' *.html | sort | uniq -c
# 死連結:0814 語言切換移除後,每檔應為 0。灰字項絕不可寫成 <a href="#">,一寫這條就紅
grep -c 'href="#"' *.html
# 0814:站上不得殘留佔位符 → 第一行應只列出 index-v1-proof.html(刻意保留),第二行應為 10
grep -l '\[TODO' *.html
grep -oh '\[TODO' index-v1-proof.html | wc -l
# 0814:`.todo` 外殼裡不得沒有佔位符 → 應為空
# ⚠ 這條抓的是「`grep [TODO` 為 0 卻仍渲染出空虛線框」的殘骸:替換佔位符時若把
#   帶 <span class="todo"> 外殼的當成純文字處理,新句子會被留在虛線框裡,
#   頁面上看起來仍是佔位符,而數 [TODO 的檢查完全看不出來(0814 verifier 抓到)。
python3 -c "import pathlib,re;print([(p.name,m[:60]) for p in pathlib.Path('.').glob('*.html') for m in re.findall(r'<span class=\"todo[^\"]*\">((?:(?!\[TODO)[^<])*?)</span>', p.read_text())])"
# 0814 稍晚:Contact 動線必須真的能寄信 → 第一行應為空(沒有按鈕還指著 #contact)、
# 第二行 40、第三行 40。⚠ 只准 header 與頁尾 Company 欄那兩條 Contact 導覽連結指向錨點
grep -n '<a class="btn[^"]*"[^>]*href="\(index\.html\)\?#contact"' *.html
grep -l 'href="mailto:salesgroup@volcatech.com' *.html | wc -l
grep -l 'href="tel:+886223279668"' *.html | wc -l
# 0814:不得殘留「這是 demo」的自白與內部導覽 → 四行皆應為空
# ⚠ 第四行是 0814 盤點補的:前三個字串沒涵蓋首頁 Trust 區底下那句「This demo loads…」,
#   結果宣稱「demo 痕跡全站零」時它還在站上
grep -n 'Demo notice\|internal design review\|are placeholders' *.html
grep -n 'This demo' *.html
grep -n 'class="wrap backlink"' *.html
grep -n 'Demo: ' *.html
# 0814:頁尾聯絡資訊已補實 → 前兩行各應輸出 40(Email 與登記地址在每頁的聯絡 dl 裡)
grep -l 'salesgroup@volcatech.com' *.html | wc -l
grep -l 'Songjiang Rd.' *.html | wc -l
# 0814 稍晚:`.legal` 灰字帶整塊移除 → 法人名 2 檔(privacy/imprint)、統編 1 檔(imprint)
# ⚠ 這三行的期望值 0814 早上是 40/40/40。改的是頁尾不是資料——法定資訊仍在 imprint.html,
#   入口是頁尾 Company 欄那兩條連結。要復原見 fix_footer_20260814.py 的 RESTORE_LEGAL
grep -l 'wrap legal' *.html | wc -l                                    # 應為 0
grep -l 'Volcatech Corporate Ltd.' *.html | wc -l                      # 應為 2
grep -l '94269177' *.html | wc -l                                      # 應為 1(imprint.html)
# ⚠ 這裡**不可以**用 `Company registration no. (Taiwan): 94269177` 當比對字串:那是
#   頁尾灰字帶的寫法,已隨灰字帶移除。imprint.html 把它拆成 <h3>欄位名</h3><p>值</p>
#   兩個節點(imprint.html:447),完整字串在站上已不存在——照舊寫法跑會得到 0 而誤判成資料掉了
grep -n 'VAT / tax ID' *.html                                          # 應為空(VAT 列已刪)
# 0814:FortiEDR 已下架 → 應為空(大小寫敏感,理由同 CE-BAS 那條)
grep -l 'FortiEDR\|fortiedr' *.html
# 舊選單術語不得殘留在「選單」→ 應輸出 0
# ⚠ 只能掃 header 區。Platform 在正文是合法英文字——gcp-vmware-engine / gcp-vertex-ai /
#   gcp-model-garden 的架構圖層名就叫 <h3>Platform</h3>,掃全檔會誤報這三頁(0806 實測)
for f in *.html; do awk '/<header/,/<\/header>/' $f; done \
  | grep -c 'Arsenal\|>Platform<\|>Operations<\|<li class="grp">'
# 19 張產品卡都有兩個出口 → 兩行皆應輸出 19
grep -oh 'Product page →' cloud-*.html | wc -l
grep -oh 'Vendor page ↗' cloud-*.html | wc -l
# 每個產品頁的架構圖都要標出主角 → 應輸出 0
# ⚠ 0806 三輪後不能再對全檔數 'node self'——.pick 的自指列也用 .node.self,會多算
for f in gcp-*.html; do awk '/<section id="stack">/,/<\/section>/' $f | grep -c 'node self'; done | grep -vc '^1$'
# 0806 三輪:19 個 gcp 頁各有 痛點/選型/FAQ 三段(pick 允許個別頁省略,目前 19 頁全有)
for s in pain pick faq; do grep -c "section id=\"$s\"" gcp-*.html | grep -vc ':1$'; done   # 三行各應輸出 0
# 資安線 6 頁各有 痛點/選型/FAQ 三段(0807 跟進 5 頁;argushack.html 0810 建頁時就帶三段)
for s in pain pick faq; do grep -c "section id=\"$s\"" sentinelone.html threatsonar.html cybereyes.html google-secops.html ess.html argushack.html | grep -vc ':1$'; done   # 三行各應輸出 0
# 0811:hero 代表事實列。24 頁各恰一列(19 GCP ＋ 5 資安;`ess.html` 與 `managed-gcp.html`
#      兩個服務／方案頁已裁決豁免,不要幫它們補)
grep -l 'class="fact"' *.html | wc -l          # 應為 24
grep -c 'class="fact"' *.html | grep -vc ':[01]$'   # 應為 0(每檔 0 或 1,不得有 2)
# 0811:hero 晶片不得放產品名(H1 已有一次,重複會讓軸 3 判 FAIL) → 應為空
# ⚠ 只能掃 .fact 那一行——`.stack` 的自我節點本來就叫產品名,掃全檔會全數誤報
for f in gcp-*.html sentinelone.html threatsonar.html cybereyes.html google-secops.html argushack.html; do
  n=$(grep -o '<h1>[^<]*</h1>' $f | sed 's/<[^>]*>//g')
  grep 'class="fact"' $f | grep -q "node self\">$n<" && echo "$f 晶片=產品名"; done
# 金額禁令(ADR 0004):單價/免費額度/促銷不上站 → 應為空
grep -nE '[$€£]|per month|free tier|free of charge' *.html
# cloud.html 的產品索引 19 列
grep -c 'Product page →' cloud.html
# 0805 移除的 4 項:選單裡應為 0,但 services.html 的頁面區塊必須還在(所以只能掃 header 區)
for f in *.html; do awk '/<header/,/<\/header>/' $f; done \
  | grep -c 'ISMS\|Penetration Testing\|Cloud FinOps\|Digital Transformation'
# 0810 全站移除的 2 項(素材不足,非否定自研):選單與頁面都不該有 → 應為空
grep -l 'AI-PTaaS\|SecPurple' *.html
# 0810 更名:CE-BAS 不得殘留在任何頁面(產品一律叫 ArgusHack)→ 應為空
# ⚠ 必須大小寫敏感,不可加 -i —— 「source-based」內含 ce-bas,加了 -i 會誤報 gcp-cloud-run.html
grep -l 'CE-BAS' *.html
# 自研宣稱不得殘留(0810:ArgusHack 是代理產品,沃凱沒有自研品在站上)→ 應為空
grep -in 'built in-house\|not resold\|we build ourselves\|self-developed' *.html
# 0811:沃凱不得出現在自己的技術夥伴清單裡(0810 撤自研宣稱時 index.html 的 partners 那列漏網,
# 上面那條 grep 掃不到「Volcatech AI」這種寫法)→ 兩行皆應為空
# ⚠ 第二條只能掃夥伴區(index 的 .vendors 那列與 V1 的 .wm 浮水印)——`<span class="vsrc">Volcatech</span>`
#   是「這項服務由沃凱提供」的合法標記,掃全檔的 >Volcatech< 會誤報 cloud/cloud-services/services 三頁
grep -n 'Volcatech AI' *.html
awk '/class="vendors"/,/<\/div>/' index.html | grep -n 'Volcatech'; grep -n 'class="wm">Volcatech' index-v1-proof.html
# 0811:佔位一律指名缺什麼(禁同義反覆的 to be confirmed;先例見 gcp-vertex-ai.html)→ 應為空
grep -n 'TODO: to be confirmed' *.html
# 佔位連結歸零 → 每檔應輸出 0
grep -c '#security-list\|#managed-list' *.html
# title 與 meta description 全站唯一 → 兩行皆應無輸出(註解宣稱兩項,指令就有兩條)
grep -h '<title>' *.html | sort | uniq -d
grep -h 'name="description"' *.html | sort | uniq -d
# aria-current 每檔=3(1 個 markup + 2 個 CSS 選擇器);四個登記在案的孤兒頁 =2
# (cloud-services / gcp-cloud-armor / privacy / imprint —— 選單沒有連結指向它們,故無 markup 那 1 個)
grep -c 'aria-current="page"' *.html
# ess.html 與 services.html 零外部連結 → 皆應輸出 0
grep -c 'https\?://' ess.html services.html
# 錨點偏移:每檔應 ≥1(缺了的話 sticky header 會蓋住 #錨點 落點)
grep -c 'scroll-margin-top' *.html
# 分層圖中連結的鍵盤焦點不被遮蔽 → 19 個 GCP 產品頁應各為 1(舊註解寫「三個」是 0806 補齊前的狀態)
grep -c '\.stack a{scroll-margin-top' gcp-*.html
# Cloud 深連結落點:22 個錨點 id 必須存在(18 GCP 產品 + Cloud Armor + 沃凱服務 3 項)
grep -ohE 'id="(compute-engine|kubernetes-engine|vmware-engine|cloud-storage|filestore|backup-dr|bigquery|pubsub|dataflow|cloud-run|app-engine|api-gateway|alloydb|cloud-sql|datastore|firestore|vertex-ai|model-garden|cloud-armor|cloud-migration|hybrid-cloud-backup|data-ai-engineering)"' \
  cloud*.html | sort -u | wc -l   # 應為 22
# 兩個總覽頁的落點:cybersecurity 6 產品 + 3 區塊、services 6 服務
# ⚠ 0810 起產品少了 ce-bas/ai-ptaas/secpurple、多了 argushack;第三個區塊 id 由 in-house 改為 validation
grep -ohE 'id="(sentinelone|threatsonar|cybereyes|google-secops|argushack)"' cybersecurity.html | sort -u | wc -l  # 應為 5(0814 FortiEDR 下架前是 6)
grep -ohE 'id="(edr|detection|validation)"' cybersecurity.html | sort -u | wc -l   # 應為 3
grep -ohE 'id="(ess|soc|isms|pentest|finops|dx|managed-gcp)"' services.html | sort -u | wc -l # 應為 7
# 37 個內容頁 footer 與 sentinelone 逐字節相同 → 應輸出 37 行 OK(排除 2 個 index*.html 與 sentinelone 自己)
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

demo 不宣稱「完全符合 WCAG 2.2 AA」。以下十項是知道且刻意留著的
(前五項無障礙、第 6–7 項一致性、第 8 項是 0812 查出的排版缺口、第 9–10 項是 0814 的內容缺口):

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
8. **全站沒有任何字體檔,IBM Plex 實際上多數訪客看不到**(2026-08-12 查出)。
   1152 處 `font-family` 100% 走 `var(--sans)`/`var(--mono)`,但 repo 內
   `.woff2`/`.woff`/`.ttf`/`.otf` **一個都沒有**、也無 `@font-face`——
   Plex 只在訪客本機剛好裝了時才生效,否則 fallback 到 `ui-sans-serif`/`system-ui`。
   **開發者看到的畫面與外部訪客很可能不同。**demo 階段刻意不修(自架字體檔會讓所有視覺
   對照多一個變因),正式 Astro 版用 `@fontsource` 自架解決;細節見
   `docs/design/00_現況基線_20260812.md` §8。

9. **ISO 27001 那一格寫「可應要求提供」,歐洲買家很可能讀成「他們沒有」**(2026-08-14)。
   首頁 Trust 區三格裡的第三格,內文是
   `Certification status, scope and certificate number are available on request.`。
   0814 grilling 時已把這個代價明白告訴使用者,使用者選擇**保留版面結構、只清掉佔位符**
   (選項 Q24a)。拿到實際認證狀態就能五分鐘換掉;在那之前**不得改寫成任何暗示已取得的說法**。
   同理 `#why` 區的 Google Cloud 夥伴等級句尾是整句刪除,站上因此**沒有任何一處說明
   沃凱與 Google 的關係**——這是已知的、待素材的空缺。

10. **`privacy.html` 有一句與託管環境綁定**(2026-08-14)。「Hosting」段寫著
   Volcatech 不會收到、不儲存、也不會併用託管商的存取紀錄——在 GitHub Pages 上這是真的
   (repo 擁有者拿不到 access log)。**換託管環境時這一句必須重新查證**,
   已登記在 `docs/待補素材清單_20260814.md` §5。

SC 1.4.13 Dismissible 原本也在這份清單上,已於 2026-08-06 修掉:`<header>` 帶一個行內
`onkeydown`,按 Esc 把焦點交給 logo(不是 `blur()`——blur 會把焦點丟回 body,
下一次 Tab 從整份文件最上面重來)。這與 navbtn 的行內 onclick 同級,不新增 `<script>` 標籤。
**滑鼠 hover 路徑仍然只能靠移開指標**,這部分未解。
