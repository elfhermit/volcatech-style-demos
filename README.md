# Volcatech 官網風格 Demos(4 styles)

同一套網站骨架(內容、選單、資訊架構相同),四種歐洲設計風格的靜態 demo,用於內部評選最終視覺方向。

| 風格 | 路徑 | 一句話定位 |
|---|---|---|
| Style 1 — Zurich Grid(瑞士型錄) | `style-1-zurich/` | 精準理性,型錄索引碼 + 細網格 |
| Style 2 — Nordic Calm(北歐留白) | `style-2-nordic/` | 沉靜信任,目錄式 Hero |
| Style 3 — SOC Console(深色主控台) | `style-3-soc/` | 戰情室語彙,mono 狀態列 + 琥珀訊號色 |
| Style 4 — Continental Spec(DIN 規格書) | `style-4-continental/` | 工程文件可信感,規格表卡片 + 紅規線 |

每個風格含兩頁:`index.html`(首頁)與 `sentinelone.html`(產品頁範例)。
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
5. 公司資料佔位:全域搜尋 `[TODO]` 逐一替換(統編 / VAT / 地址 / 認證等)。

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

- 每風格僅實作 2 頁;導覽列中只有 **Home** 與 **SentinelOne** 可點,其餘連結為示意
  (`href="#"`,游標停留顯示 “Demo scope”)。
- **語言切換(EN|繁中)為視覺示意**,實際 i18n 於正式 Astro 版實作。
- **字體**:demo 以系統字體近似呈現(已宣告目標字體名稱,若本機安裝則直接套用)。
  正式版依規格以 `@fontsource` 自行代管 Space Grotesk / Source Serif 4 / IBM Plex / Barlow / Inter
  (GDPR:不外連 Google Fonts CDN)。
- 手機版(<768px 或 <900px)導覽列收合為 Menu 按鈕;下拉選單支援滑鼠 hover 與鍵盤 focus。
- 公司事實(統編、地址、認證等)以 `[TODO]` 佔位,未經確認不虛構。

---

## 4. 評選建議

1. **3 秒測試**:遮住 logo 給不知情的人看首屏 3 秒,要能答出「賣雲端 + 資安產品 + 資安服務」。
2. 想像收件人是**歐洲企業的資安主管**——哪一版讓他覺得「這家懂我們」?
3. 手機 390px 寬再看一次。
4. 深色的 Style 3 特別檢查長文閱讀舒適度。
5. 想像名片、簡報、提案書套用同風格是否成立。

---

## 5. 選出風格之後(正式版)

1. 開啟 `docs/Volcatech_多風格_Build_Prompts.md`。
2. 複製【A. 共用基底 Prompt】+ 勝出的【風格模組】,一起貼給 Claude Code。
3. 產出完整 Astro 版(11 個產品/服務頁 ×2 語系、GDPR 隱私頁、sitemap/hreflang、
   GitHub Actions 自動部署),再依 `docs/官網建置計畫_Build_Prompt_v3.md` 的
   §7 里程碑與 §9 驗收清單走完,最後按 §6.5 做 volcatech.com 網域切換與 301 轉址。

---

## 6. 專案結構

```text
Volcatech_Web/                  # 專案根(= VS Code 開啟此層、http.server 起在此層)
├── index.html                  # 風格總覽入口
├── README.md
├── CLAUDE.md                   # Claude Code 自動讀取的專案規則
├── .gitignore
├── .vscode/                    # VS Code:建議延伸模組、設定、預覽 Task
│   ├── extensions.json
│   ├── settings.json
│   └── tasks.json
├── .github/
│   └── copilot-instructions.md # GitHub Copilot 專案指示
├── docs/
│   ├── 官網建置計畫_Build_Prompt_v3.md    # 完整計畫書(v3)
│   ├── Volcatech_多風格_Build_Prompts.md  # 基底 + 4 風格模組(產正式版用)
│   └── 接手開發_Prompts.md                # VS Code 內 AI 協作的現成 prompts
├── style-1-zurich/       index.html · sentinelone.html
├── style-2-nordic/       index.html · sentinelone.html
├── style-3-soc/          index.html · sentinelone.html
└── style-4-continental/  index.html · sentinelone.html

(未來)└── site/               # 勝出風格的正式 Astro 版,獨立於本 demo 不混改
```
