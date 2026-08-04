# Volcatech 官網 Demo — 勝出風格 style-3-soc(SOC Console)

**2026-07-31 內部評選已結束**:勝出組合為 **Style 3 — SOC Console(深色主控台)色系 × 原版直落版型**,
色系凍結。現行維護對象只有 `style-3-soc/`(15 頁),目前正在比對**兩個選單變體**(Nav A / Nav B)
擇一定稿;其餘風格與版型的評選歷史已全部移入 `archive/`(凍結,不再更新)。

| 現行 demo(15 頁) | 路徑 | 說明 |
|---|---|---|
| 首頁 Nav A — 單層下拉 | `style-3-soc/index.html` | 頂部選單 `Google Cloud / CyberSecurity / Services`,下拉內以 mono 小標分組 |
| 首頁 Nav B — 二層 flyout | `style-3-soc/index-nav-b.html` | 選單內容同 Nav A,分組升級為第二層 flyout(hover / `:focus-within` 展開) |
| Cloud 總覽 ×1 | `cloud.html` | 代碼 CI;h1 `Cloud Infrastructure`。六分類導覽 + 沃凱雲端服務 |
| Cloud 分類頁 ×7 | `cloud-compute.html`、`cloud-storage.html`、`cloud-analytics.html`、`cloud-serverless.html`、`cloud-databases.html`、`cloud-ai.html`、`cloud-services.html` | 代碼 CI-01〜CI-07;各頁收錄該分類的 GCP 產品(每項一個錨點),`cloud-services.html` 另含 Cloud Armor 與沃凱自有雲端服務 3 項 |
| 產品頁 ×4 | `sentinelone.html`、`threatsonar.html`、`cybereyes.html`、`google-secops.html` | 均用 Nav A |
| 方案頁 ×1 | `ess.html` | **Enterprise Security Service(ESS)**:沃凱打包方案(CyberEyes WDR + 多品牌 EDR + 自有 7x24 SOC)。**方案層,不屬 19 項 SKU**;全頁零外部連結;用 Nav A |

兩個首頁變體自 `<main>` 起**逐字節相同**(一致性鐵則),差異只在 header/nav;
hero 文案(H1 / 副標 / CTA)為會後改版的置中版。選單分類 `CyberSecurity` 的駝峰寫法
是會議指定的**刻意寫法**(僅限選單分類名;H1 等內文仍為定稿原文)。
入口總覽:根目錄 `index.html`(Demo hub,主卡含上述 15 頁連結)。

## 評選歷史(已結束,存檔於 `archive/`)

評選分兩輪:第一輪比「色系與視覺語彙」(Style 1–4),第二輪固定色系、只換版型框架
(Layout 1–4,與同號 Style 形成唯一變因為版型的對照組);所有版本資訊架構與文案逐字一致。
0731 會議選定 Style 3 色系 × 原版直落版型後,以下內容已全數歸檔且**凍結不再更新**:

- 落選風格:`archive/style-1-zurich/`、`archive/style-2-nordic/`、`archive/style-4-continental/`
- 版型變體:`archive/layout-1-magazine-zurich/`、`archive/layout-2-split-nordic/`、
  `archive/layout-3-bento-soc/`、`archive/layout-4-sidebar-continental/`
- 外部 AI 參考組:`archive/Volcatech_Layout_Variants_GPT/`(GPT 依同規格產出的實作,
  **維持唯讀:不修改、不 review**,規則見 `CLAUDE.md` 專節)
- 舊評選總覽:`archive/index.html`(帶已歸檔橫幅)

---

## 0. 用 VS Code 接手開發(建議流程)

1. VS Code →「File → Open Folder…」開啟本專案資料夾 `Volcatech_Web/`(即本 README 所在層)。
2. 右下角會提示安裝**建議延伸模組**(來自 `.vscode/extensions.json`):
   **Claude Code**、Live Server、Prettier——按「Install All」即可。
3. 預覽方式擇一:
   - 對任一 `.html` 按右鍵 → **Open with Live Server**(存檔自動重新整理);
   - 或 `Terminal → Run Task… → Serve demos (http://localhost:8000)`(已內建於 `.vscode/tasks.json`)。
4. AI 協作:**Claude Code 會自動讀取根目錄 `CLAUDE.md`**(專案背景 + 硬性規則 + tokens 速查),
   直接下指令即可;常見任務的現成 prompt 在 `docs/接手開發_Prompts.md`。GitHub Copilot 使用者由
   `.github/copilot-instructions.md` 自動套用相同規則。
5. 公司資料佔位:全域搜尋 `[TODO` 逐一替換(註冊地址 / 統編 / VAT / Email / 電話 / 認證等)。
   全案只用 `[TODO: 說明]` 一種語法。公司事實來源為 `docs/公司_104.md`,
   但該檔只可用於服務範圍與願景,**法定資訊必須由公司提供**。

---

## 1. 本機預覽

**方法 A(最快)**:直接用瀏覽器開啟根目錄的 `index.html`(雙擊即可),
從 Demo hub 點進 style-3 的 15 個頁面(兩個選單變體、8 個 Cloud 頁、4 個產品頁、ESS 方案頁)與歸檔區。

**方法 B(建議,行為與正式環境一致)**:

```bash
# 在專案根目錄(本 README 所在層)執行
python3 -m http.server 8000
# 瀏覽器開啟:
#   http://localhost:8000/                              → Demo hub
#   http://localhost:8000/style-3-soc/                  → 首頁 Nav A(單層下拉)
#   http://localhost:8000/style-3-soc/index-nav-b.html  → 首頁 Nav B(二層 flyout)
#   http://localhost:8000/style-3-soc/cloud.html        → Cloud 總覽(CI)
#   http://localhost:8000/style-3-soc/cloud-compute.html    → Cloud 分類頁:Compute(CI-01)
#   http://localhost:8000/style-3-soc/cloud-storage.html    → Cloud 分類頁:Storage(CI-02)
#   http://localhost:8000/style-3-soc/cloud-analytics.html  → Cloud 分類頁:Analytics(CI-03)
#   http://localhost:8000/style-3-soc/cloud-serverless.html → Cloud 分類頁:Serverless(CI-04)
#   http://localhost:8000/style-3-soc/cloud-databases.html  → Cloud 分類頁:Databases(CI-05)
#   http://localhost:8000/style-3-soc/cloud-ai.html         → Cloud 分類頁:AI(CI-06)
#   http://localhost:8000/style-3-soc/cloud-services.html   → Cloud 分類頁:Cloud services & Cloud Armor(CI-07)
#   http://localhost:8000/style-3-soc/sentinelone.html  → 產品頁:SentinelOne
#   http://localhost:8000/style-3-soc/threatsonar.html  → 產品頁:ThreatSonar
#   http://localhost:8000/style-3-soc/cybereyes.html    → 產品頁:CyberEyes
#   http://localhost:8000/style-3-soc/google-secops.html → 產品頁:Google SecOps
#   http://localhost:8000/style-3-soc/ess.html          → 方案頁:ESS
#   http://localhost:8000/archive/                      → 舊評選總覽(已凍結)
```

---

## 2. 部署到 GitHub Pages(demo 對外展示用)

純靜態 HTML,**零建置設定**,推上去即可用。部署方式不變;
`style-3-soc/` 的線上路徑不變,被歸檔的頁面網址前多一層 `/archive/`。

**發布範圍**:`docs/` 已列入 `.gitignore` —— 內部建置計畫與規格書**不推上 public repo**
(本機檔案仍保留)。`.nojekyll` 空檔案的作用是關閉 GitHub Pages 的 Jekyll 處理,
讓所有檔案原樣提供(也讓未來 Astro 版的 `_astro/` 目錄不被忽略)。

```bash
# 在專案根目錄執行
git init
git add .
git commit -m "Volcatech website style demos (4 styles)"
git branch -M main

# 建 repo 並推送(gh CLI 已登入時最快,會自動設 remote)
gh repo create volcatech-style-demos --public --source=. --remote=origin --push

# 啟用 Pages(main / root)
gh api -X POST repos/{owner}/volcatech-style-demos/pages \
  -f 'source[branch]=main' -f 'source[path]=/'
```

沒有 gh CLI 時:先在 GitHub 網頁手動建立空 repo(不要勾 Add README),然後

```bash
git remote add origin https://github.com/<帳號>/volcatech-style-demos.git
git push -u origin main
```

再到該 repo → **Settings → Pages** → Source 選 `Deploy from a branch`,
Branch 選 `main` / `/(root)` → Save。

約 1–2 分鐘後網址為:`https://<帳號>.github.io/volcatech-style-demos/`
(全站皆使用相對路徑,放在任何子路徑下都能正常運作。)

**後續更新**:改完檔案後 `git add -A && git commit -m "訊息" && git push`,
Pages 約 1 分鐘後自動更新(若沒變,瀏覽器強制重新整理 Cmd+Shift+R)。

---

## 3. Demo 範圍與已知限制

- 現行 demo 共 15 頁(兩個首頁選單變體 + 8 個 Cloud 頁 + 4 個產品頁 + 1 個方案頁)。
  **選單沒有死連結**:**Google Cloud** 下拉的 18 項 GCP 產品全部是深連結
  (`分類頁#產品錨點`,例 `cloud-compute.html#compute-engine`);
  **SentinelOne / ThreatSonar / CyberEyes / Google SecOps** 有獨立產品頁、
  **ESS** 有獨立方案頁,在全站 nav 與 footer 都連真頁;其餘尚無獨立頁的服務,
  選單連結捲到首頁對應區塊(`index.html#offer` / `#built`);
  Privacy Policy 與 Imprint 指向頁尾法定資訊區(`#legal`),正式版才有獨立頁面。
- **選單內容(兩變體逐字相同)**:`Google Cloud` 下拉 = 頂部 Overview 入口(`cloud.html`)
  加上八組 22 項(GCP 產品樹六組 18 項:Compute / Storage / Analytics / Serverless /
  Databases / AI;另加 Edge security 1 項與 Volcatech cloud services 3 項);
  `CyberSecurity` = 8 項三組(Endpoint — EDR / **Detection — SIEM & WDR** / Built in-house;
  CyberEyes 實為 WDR,故 SIEM 群組已改名,白話行為
  `CyberSecurity — EDR · SIEM & WDR · Built in-house`);
  `Services` = 「Enterprise Security Service (ESS)」置頂 + 原 5 項。
  每個下拉第一行仍是 mono 白話對照。
- **頁尾「Cloud Infrastructure」欄**已改為 8 行分類連結(Overview / Compute / Storage /
  Analytics / Serverless / Databases / AI / Cloud services & Cloud Armor),
  取代舊的 6 項 SKU 列法。
- `cloud-services.html` 的沃凱自有雲端服務 3 項(Cloud Migration & Kubernetes /
  Hybrid Cloud & Backup / Data & AI Engineering)內文為 `[TODO: service description]`
  佔位——素材待補,是**已知待辦**而非疏漏。該頁另有 1 條指向 Cloud Armor 官方頁的外部連結
  (零外部連結規則只適用 `ess.html`)。
- **語言切換(EN / 繁中)**已是真連結與正確的 `lang` / `hreflang` 標記,
  但繁中版本於正式 Astro 版才會產出(游標停留有說明)。
- **字體**:demo 以系統字體近似呈現(已宣告目標字體名稱,若本機安裝則直接套用)。
  正式版依規格以 `@fontsource` 自行代管 IBM Plex Sans / IBM Plex Mono
  (GDPR:不外連 Google Fonts CDN)。
- 手機版導覽列收合為 Menu 按鈕(選單本身可捲動);
  下拉選單支援滑鼠 hover 與鍵盤 focus(`:focus-within`),Nav B 的第二層 flyout 同樣支援。
- 公司事實(註冊地址、統編、VAT、Email、電話、ISO 認證等)以 `[TODO: 說明]` 佔位,未經確認不虛構。
  **對外分享 demo 前,建議至少先取得可用的聯絡 Email 與電話**,否則頁尾整片佔位觀感不佳。
- `archive/` 內全部內容(落選風格、版型變體、GPT 參考包、舊總覽)已凍結:
  不修改、不 review、不納入任何檢查;其中 GPT 參考包自帶的 `CLAUDE.md` / `README.md` /
  `HANDOVER.md` 只描述它自己,**不適用本專案**,規則衝突以根目錄 `CLAUDE.md` 為準。

---

## 4. 選單變體定稿之後(正式版)

1. 開啟 `docs/Volcatech_多風格_Build_Prompts.md`(**全案唯一事實來源**)。
2. 複製【A. 共用基底 Prompt】+ 勝出的【風格 3(SOC Console)模組】,一起貼給 Claude Code。
   **注意**:該檔 §B 的 style-3 選單定義(`Platform / Arsenal / Operations`)是評選期歷史;
   0731 會後選單分類已改為 `Google Cloud / CyberSecurity / Services`(含 GCP 產品樹),
   **現行選單以 `style-3-soc/` 頁面為準**。
3. 產出完整 Astro 版(19 個產品/服務頁 ×2 語系、3 個總覽頁、GDPR 隱私頁與 Imprint、
   sitemap/hreflang、GitHub Actions 自動部署),再依同檔的【品質底線(驗收)】逐項自檢。

> `docs/官網建置計畫_Build_Prompt_v3.md` 已凍結為 **legacy**:其產品數量(9/11 項)、
> 資訊架構(`Solutions` 下拉)、路由、content schema 與 §9 驗收清單**皆已失效**,
> 照做會把清單砍回舊規格。該檔僅保留為背景脈絡與網域切換/301 轉址(§6.5)的參考。

---

## 5. 專案結構

```text
Volcatech_Web/                  # 專案根(= VS Code 開啟此層、http.server 起在此層)
├── index.html                  # Demo hub:style-3 主卡(雙變體連結)+ 歸檔入口
├── README.md
├── CLAUDE.md                   # Claude Code 自動讀取的專案規則
├── HANDOVER.md                 # 進度與接手指引(速查;規格正本在 docs/)
├── .gitignore
├── .nojekyll                   # 關閉 GitHub Pages 的 Jekyll 處理,勿刪
├── .vscode/                    # VS Code:建議延伸模組、設定、預覽 Task
│   ├── extensions.json
│   ├── settings.json
│   └── tasks.json
├── .github/
│   └── copilot-instructions.md # GitHub Copilot 專案指示
├── docs/                       # 不隨 demo 發布(已列入 .gitignore)
│   ├── Volcatech_多風格_Build_Prompts.md  # ★ 唯一事實來源:基底 + 風格模組(§B style-3 選單定義為評選期歷史)
│   ├── Volcatech_版型變體_Build_Prompts.md # 版型變體正本(評選歷史,對應 archive/ 內 layout 資料夾)
│   ├── 版型框架挑選指南.md                 # 版型科普與挑選依據(評選歷史)
│   ├── 版型變體_外部AI_Prompt_Pack.md      # 自足式 prompt 匯出品(評選歷史)
│   ├── meeting_0731.md                    # 0731 評選會議紀錄
│   ├── Cloud線_內容規劃_20260804.md        # Cloud 線 8 頁的內容正本(2026-08-04)
│   ├── 公司_104.md                        # 公司事實來源(服務範圍與願景)
│   ├── 接手開發_Prompts.md                # VS Code 內 AI 協作的現成 prompts
│   ├── 官網建置計畫_Build_Prompt_v3.md    # legacy(已凍結,規格失效,僅供背景)
│   ├── product/                           # 產品素材與簡述(索引:README;素材統一入口:產品簡介總覽.md)
│   ├── (其餘會議/優化筆記若干)
│   └── backups/                           # 制度檔修改前備份
├── style-3-soc/                # ★ 勝出風格(現行唯一維護對象,共 15 頁)
│   ├── index.html              # 首頁 Nav A(單層下拉、mono 小標分組)
│   ├── index-nav-b.html        # 首頁 Nav B(二層 flyout);<main> 起與 Nav A 逐字節相同
│   ├── cloud.html              # Cloud 總覽(CI):六分類導覽 + 沃凱雲端服務
│   ├── cloud-compute.html      # Cloud 分類頁 CI-01:Compute Engine / Kubernetes Engine / VMware Engine
│   ├── cloud-storage.html      # Cloud 分類頁 CI-02:Cloud Storage / Filestore / Backup and DR
│   ├── cloud-analytics.html    # Cloud 分類頁 CI-03:BigQuery / Pub/Sub / Dataflow
│   ├── cloud-serverless.html   # Cloud 分類頁 CI-04:Cloud Run / App Engine / API Gateway
│   ├── cloud-databases.html    # Cloud 分類頁 CI-05:AlloyDB / Cloud SQL / Datastore / Firestore
│   ├── cloud-ai.html           # Cloud 分類頁 CI-06:Vertex AI / Model Garden
│   ├── cloud-services.html     # Cloud 分類頁 CI-07:Cloud Armor + 沃凱雲端服務 3 項([TODO] 待補內文)
│   ├── sentinelone.html        # 產品頁(用 Nav A,下同)
│   ├── threatsonar.html        # 產品頁
│   ├── cybereyes.html          # 產品頁
│   ├── google-secops.html      # 產品頁
│   └── ess.html                # 方案頁:ESS(方案層,非 19 項 SKU;全頁零外部連結)
├── archive/                    # 評選歷史,全部凍結不再更新
│   ├── index.html              # 舊評選總覽(帶已歸檔橫幅)
│   ├── style-1-zurich/
│   ├── style-2-nordic/
│   ├── style-4-continental/
│   ├── layout-1-magazine-zurich/
│   ├── layout-2-split-nordic/
│   ├── layout-3-bento-soc/
│   ├── layout-4-sidebar-continental/
│   └── Volcatech_Layout_Variants_GPT/  # 外部 AI 參考組:唯讀,不修改、不 review

(未來)└── site/               # 正式 Astro 版,獨立於本 demo 不混改
```
