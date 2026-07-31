# Volcatech 官網風格 Demos(4 styles + 4 layouts)

**資訊架構與文案完全相同**(3 條業務板塊 / 19 項服務 / 共用 H1 與所有內文,所有版本逐字一致),
**只有導覽的組織方式與視覺呈現不同**——靜態 demo,用於內部評選最終視覺方向。評選分兩輪:
第一輪比「色系與視覺語彙」(Style 1–4),第二輪固定色系、**只換版型框架**(Layout 1–4,
與同號 Style 形成唯一變因為版型的對照組)。評選時請只比較「看起來與用起來」,不要比文案。

| 風格 | 路徑 | 一句話定位 | 導覽結構 |
|---|---|---|---|
| Style 1 — Zurich Grid(瑞士型錄) | `style-1-zurich/` | 精準理性,型錄索引碼 + 細網格 | 扁平型錄索引:`(C)` / `(E·S·A)` / `(X)` 三下拉 |
| Style 2 — Nordic Calm(北歐留白) | `style-2-nordic/` | 沉靜信任,目錄式 Hero | 單一 Mega-menu「What We Offer」,展開 3 欄 |
| Style 3 — SOC Console(深色主控台) | `style-3-soc/` | 戰情室語彙,mono 狀態列 + 琥珀訊號色 | 維運術語 Platform / Arsenal / Operations |
| Style 4 — Continental Spec(DIN 規格書) | `style-4-continental/` | 工程文件可信感,規格表卡片 + 紅規線 | 雙層 header + `§1`–`§3` 章節編號 |

每個風格含兩頁:`index.html`(首頁)與 `sentinelone.html`(產品頁範例)。

| 版型變體(第二輪) | 路徑 | 版型框架 | 沿用色系 |
|---|---|---|---|
| Layout 1 — Magazine Editorial | `layout-1-magazine-zurich/` | 雜誌編輯式:超大 H1 + 三欄目錄 + 序號章節 | Style 1 |
| Layout 2 — Split & Zig-zag | `layout-2-split-nordic/` | 分割式 hero + 交錯圖文 | Style 2 |
| Layout 3 — Bento Grid | `layout-3-bento-soc/` | 儀表板卡牆,一屏總覽(深色) | Style 3 |
| Layout 4 — Fixed Sidebar | `layout-4-sidebar-continental/` | 左側常駐 `§1`–`§3` 目錄側欄 | Style 4 |

每個版型變體含五頁:`index.html`、`sentinelone.html`、`services.html`、`about.html`、`contact.html`。
入口總覽:根目錄 `index.html`。

---

## 0. 用 VS Code 接手開發(建議流程)

1. VS Code →「File → Open Folder…」開啟本專案資料夾 `Volcatech_Web/`(即本 README 所在層)。
2. 右下角會提示安裝**建議延伸模組**(來自 `.vscode/extensions.json`):
   **Claude Code**、Live Server、Prettier——按「Install All」即可。
3. 預覽方式擇一:
   - 對任一 `.html` 按右鍵 → **Open with Live Server**(存檔自動重新整理);
   - 或 `Terminal → Run Task… → Serve demos (http://localhost:8000)`(已內建於 `.vscode/tasks.json`)。
4. AI 協作:**Claude Code 會自動讀取根目錄 `CLAUDE.md`**(專案背景 + 硬性規則 + tokens 速查),
   直接下指令即可;常見任務(微調風格、補產品頁、混搭、產正式 Astro 版、推 GitHub)的
   **現成 prompt 在 `docs/接手開發_Prompts.md`**。GitHub Copilot 使用者由
   `.github/copilot-instructions.md` 自動套用相同規則。
5. 公司資料佔位:全域搜尋 `[TODO` 逐一替換(註冊地址 / 統編 / VAT / Email / 電話 / 認證等)。
   全案只用 `[TODO: 說明]` 一種語法。公司事實來源為 `docs/公司_104.md`,
   但該檔只可用於服務範圍與願景,**法定資訊必須由公司提供**。

---

## 1. 本機預覽

**方法 A(最快)**:直接用瀏覽器開啟根目錄的 `index.html`(雙擊即可),從總覽頁點進各風格。

**方法 B(建議,行為與正式環境一致)**:

```bash
# 在專案根目錄(本 README 所在層)執行
python3 -m http.server 8000
# 瀏覽器開 http://localhost:8000
```

---

## 2. 部署到 GitHub Pages(demo 對外展示用)

純靜態 HTML,**零建置設定**,推上去即可用。

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

- 每風格(Style)實作 2 頁、每版型變體(Layout)實作 5 頁。**選單沒有死連結**:
  只有 **SentinelOne** 有獨立產品頁;Style 版其餘 18 項服務的選單連結捲到首頁對應區塊
  (`index.html#offer` / `#built`),Layout 版則指到 `services.html#<slug>` 服務總覽錨點;
  Privacy Policy 與 Imprint 指向頁尾法定資訊區(`#legal`),正式版才有獨立頁面。
- **語言切換(EN / 繁中)**已是真連結與正確的 `lang` / `hreflang` 標記,
  但繁中版本於正式 Astro 版才會產出(游標停留有說明)。
- **字體**:demo 以系統字體近似呈現(已宣告目標字體名稱,若本機安裝則直接套用)。
  正式版依規格以 `@fontsource` 自行代管 Space Grotesk / Source Serif 4 / IBM Plex / Barlow / Inter
  (GDPR:不外連 Google Fonts CDN)。
- 手機版(<860px 或 <900px)導覽列收合為 Menu 按鈕(選單本身可捲動);
  下拉選單支援滑鼠 hover 與鍵盤 focus(`:focus-within`)。
- 公司事實(註冊地址、統編、VAT、Email、電話、ISO 認證等)以 `[TODO: 說明]` 佔位,未經確認不虛構。
  **對外分享 demo 前,建議至少先取得可用的聯絡 Email 與電話**,否則頁尾整片佔位觀感不佳。

---

## 4. 評選建議

1. **3 秒測試**:遮住 logo 給不知情的人看首屏 3 秒,要能答出「賣**雲端 + 資安 + 託管維運**」。
2. **觸達性測試**:從首頁出發,**2 次點擊內**要找得到「24/7 SOC」與「上雲搬遷(Cloud Migration)」。
3. 想像收件人是**歐洲企業的資安主管**——哪一版讓他覺得「這家懂我們」?
4. 手機 390px 寬再看一次(重點:Style 2 的 19 項 mega-menu、Style 4 的雙層 header 收合後)。
5. 深色的 Style 3 特別檢查長文閱讀舒適度。
6. 想像名片、簡報、提案書套用同風格是否成立。

**三個刻意變因(評選時請忽略,不要當成優劣)**:Style 4 的 CTA 用 `Request a proposal`
(其餘三風格用 `Contact us`);Style 2 沒有頂層 `Home`(logo 即入口);
Style 3 用 `Arsenal` 等維運術語(每個下拉首行都附白話對照)。
除此之外**所有文案四風格逐字相同**。

---

## 5. 選出風格之後(正式版)

1. 開啟 `docs/Volcatech_多風格_Build_Prompts.md`(**全案唯一事實來源**)。
2. 複製【A. 共用基底 Prompt】+ 勝出的【風格模組】,一起貼給 Claude Code。
3. 產出完整 Astro 版(19 個產品/服務頁 ×2 語系、3 個總覽頁、GDPR 隱私頁與 Imprint、
   sitemap/hreflang、GitHub Actions 自動部署),再依同檔的【品質底線(驗收)】逐項自檢。

> `docs/官網建置計畫_Build_Prompt_v3.md` 已凍結為 **legacy**:其產品數量(9/11 項)、
> 資訊架構(`Solutions` 下拉)、路由、content schema 與 §9 驗收清單**皆已失效**,
> 照做會把清單砍回舊規格。該檔僅保留為背景脈絡與網域切換/301 轉址(§6.5)的參考。

---

## 6. 專案結構

```text
Volcatech_Web/                  # 專案根(= VS Code 開啟此層、http.server 起在此層)
├── index.html                  # 風格總覽入口
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
│   ├── Volcatech_多風格_Build_Prompts.md  # ★ 唯一事實來源:基底 + 4 風格模組
│   ├── Volcatech_版型變體_Build_Prompts.md # ★ 版型變體(layout-*)正本:基底 + 4 版型模組
│   ├── 版型框架挑選指南.md                 # 版型科普與挑選依據(給非設計背景)
│   ├── 版型變體_外部AI_Prompt_Pack.md      # 自足式 prompt 匯出品(給 ChatGPT/Gemini 用)
│   ├── 公司_104.md                        # 公司事實來源(服務範圍與願景)
│   ├── 接手開發_Prompts.md                # VS Code 內 AI 協作的現成 prompts
│   ├── 官網建置計畫_Build_Prompt_v3.md    # legacy(已凍結,規格失效,僅供背景)
│   └── backups/                           # 制度檔修改前備份
├── style-1-zurich/       index.html · sentinelone.html
├── style-2-nordic/       index.html · sentinelone.html
├── style-3-soc/          index.html · sentinelone.html
├── style-4-continental/  index.html · sentinelone.html
├── layout-1-magazine-zurich/     ┐
├── layout-2-split-nordic/        │ 各 5 頁:index · sentinelone ·
├── layout-3-bento-soc/           │ services · about · contact
└── layout-4-sidebar-continental/ ┘

(未來)└── site/               # 勝出風格的正式 Astro 版,獨立於本 demo 不混改
```
