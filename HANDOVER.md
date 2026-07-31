# Volcatech 官網風格 Demo 接手指引 (Handover)

> **最後更新**：2026-07-30
> **本檔定位**：進度速查與接手指令集。
> **規格正本是 `docs/Volcatech_多風格_Build_Prompts.md`**——本檔與它衝突時，一律以它為準。

---

## 1. 目前狀態

4 個歐洲風格 demo（每風格 `index.html` + `sentinelone.html`，共 8 頁）已完成
**3 板塊重構、Top Menu 差異化、歐規頁尾與文件收斂**。

### 定調的資訊架構（四風格共用，不得各改各的）

- **3 條業務板塊**：`Cloud Infrastructure` / `Cybersecurity` / `Managed Services`
- **19 項服務**（清單與 slug 見規格正本 §A）：Cloud 6 + Cybersecurity 8 + Managed 5
- 自研 **CE-BAS / AI-PTaaS / SecPurple** 屬 Cybersecurity 底下的第三個群組，
  但首頁另有專屬的 **Built by Volcatech** 區塊——它不是第 4 條產品線，**不進頂層導覽**
- **共用文案逐字相同**：H1、副標、三線區、Built by Volcatech 三品描述、Why 三點、
  Trust 行、CTA band 標題、footer legal block
- **section 順序四檔一致**：`top` → `offer` → `built` → `why` → `trust` → `vendors` → `contact` → `legal`

### 本輪完成的事

1. **板塊從 4 條收斂為 3 條**，修掉 style-4「導覽 4 板塊 vs hero 3 卡」的自相矛盾。
2. **服務清單依 `docs/公司_104.md` 擴充到 19 項**，補上先前站上完全沒有的：
   上雲搬遷 & Kubernetes、混合雲 & 備份、Data & AI 工程（ETL／大數據／ML／GenAI）、
   雲端 FinOps & 教育訓練。
3. **四風格 Top Menu 差異化**（逐字定義見規格正本 §B）：
   - Zurich：扁平型錄索引 `(C)` / `(E·S·A)` / `(X)` 三下拉，**補上先前完全缺失的 Managed Services 層級**
   - Nordic：單一 `What We Offer` Mega-menu，展開 3 欄 = 6 / 8 / 5 項；無頂層 `Home`
   - SOC：`Platform` / `Arsenal` / `Operations`，每個下拉首行為 mono 狀態列的白話對照
   - Continental：雙層 header + `§1`–`§3` 章節編號 + `Company` 下拉，AI 三品編為 §2.3
4. **修掉四風格文案不一致**：H1／CTA 統一（Contact us，sentence case），
   拆開 style-3 合併的 Trust/Vendors，移除 hype（`leading vendors`）與絕對化承諾（`map every`）。
5. **歐規頁尾**：5 欄結構 + 法定資訊區（註冊地址／統編／VAT／Email／+886 電話／Privacy／Imprint／
   Demo notice），四風格內容逐字相同、呈現依風格。
6. **無障礙與法遵修正**：語言切換改真連結並補 `lang="zh-Hant-TW"`；
   修掉 style-4 手機版把 Imprint／隱私權／語言切換整條 `display:none` 的問題；
   style-3 取消正文 ALL CAPS 並修正琥珀色用於小字的自我違規；
   Nordic 的 `.arr` 位移移入 `prefers-reduced-motion` 內。
7. **死連結歸零**：18 項無獨立頁面的服務改指首頁對應區塊（`index.html#offer` / `#built`），
   每檔僅剩語言切換的 1 個 `href="#"`（style-4 因雙處切換器為 2）。
8. **文件收斂**：`docs/Volcatech_多風格_Build_Prompts.md` 立為唯一事實來源並重寫；
   `docs/官網建置計畫_Build_Prompt_v3.md` 標為 legacy；
   CLAUDE.md／README.md／`.github/copilot-instructions.md`／`docs/接手開發_Prompts.md`／
   根 `index.html` 全部同步（產品數量從先前 6 份檔案 6 種說法統一為 19）。
   佔位語法統一為 `[TODO: 說明]`（不再有 `{{TODO}}`）。

---

## 2. 各風格導覽結構速查

> 逐字定義（含所有下拉項目文字）以 `docs/Volcatech_多風格_Build_Prompts.md` §B 為準，本表僅速查。

| 風格 | 頂層結構 | 簽名元素 |
|---|---|---|
| **Style 1 Zurich** | `Home` \| `(C) Cloud Infrastructure ▾` \| `(E·S·A) Cybersecurity ▾` \| `(X) Managed Services ▾` \| `About` \| `[Contact us]` \| `EN 繁中` | 型錄索引碼、hairline 網格 |
| **Style 2 Nordic** | `Volcatech` \| `What We Offer ▾`（3 欄 Mega-menu） \| `About` \| `[Contact us]` \| `EN 繁中` | 目錄式 Hero、無頂層 Home |
| **Style 3 SOC** | `● VOLCATECH` \| `Home` \| `Platform ▾` \| `Arsenal ▾` \| `Operations ▾` \| `About` \| `[Contact us]` \| `EN 繁中` | mono 狀態列、狀態綠圓點、琥珀訊號色 |
| **Style 4 Continental** | 上層：公司名 · Imprint · Privacy · `EN 繁中`／下層：`Home` \| `§1` \| `§2` \| `§3` \| `Company ▾` \| `[Request a proposal]` | 雙層 header、DIN § 編號、表格式 legal block |

### 三個刻意變因（評選時請忽略）

`Request a proposal`（僅 style-4）、無頂層 `Home`（僅 style-2）、`Arsenal` 等維運術語（僅 style-3）。
除此之外所有文案四風格逐字相同——評選比的是視覺與導覽體驗，不是文案。

---

## 3. 待辦（Roadmap）

- [ ] **任務 1：內部評選選出勝出風格**（Style 1 / 2 / 3 / 4 擇一）。
      評選方式見 `docs/Volcatech_多風格_Build_Prompts.md` §C 與根 `index.html` 的說明區。
- [ ] **任務 2：補齊其餘 18 個產品/服務頁**（目前僅 `sentinelone.html`）。用下方 Prompt B。
- [ ] **任務 3：向公司取得法定資訊並替換 `[TODO`**：
      註冊地址、統一編號、VAT／稅籍編號、對外聯絡 Email、電話（+886 國際格式）。
      另外 **ISO 27001 等認證狀態**與 **Google Cloud 合作等級**未經確認**絕不可寫上去**。
      注意：`docs/公司_104.md` 是公司自述，**不是法定登記資料**，不能拿來填統編或地址。
- [x] **任務 1b：版型變體 demo（第二輪評選）——已實作（2026-07-31）**：
      固定 4 套色系、只換版型框架，每變體 5 頁（首頁＋SentinelOne＋services＋about＋contact），
      建於 `layout-*/`，與 `style-*/` 形成一對一的純版型對照組。機械驗收（文案逐字 ×8 首頁、
      section 順序、19 錨點、無外部資源、標籤配對）全數通過；**瀏覽器層（390px 無水平捲軸、
      對比、鍵盤走查）仍需人工確認**。規格正本 `docs/Volcatech_版型變體_Build_Prompts.md`；
      挑選背景 `docs/版型框架挑選指南.md`；給外部 AI（ChatGPT/Gemini）跑的自足式 prompt 在
      `docs/版型變體_外部AI_Prompt_Pack.md`。
- [ ] **任務 4：建置正式版 Astro 專案**於 `site/`。用下方 Prompt C。
- [ ] （未來）繁體中文版與更多語系：i18n 架構已要求語系清單集中於單一陣列，新增語系不需改元件。

---

## 4. 可直接複製給下一位 AI 的 Prompts

### Prompt A：預覽與驗收檢查

```text
請讀取根目錄的 HANDOVER.md 與 CLAUDE.md。
用 python3 -m http.server 8000 啟動本機伺服器，對 4 個風格
（style-1-zurich、style-2-nordic、style-3-soc、style-4-continental）的
index.html 與 sentinelone.html 做檢查：
① HTML 標籤配對（python html.parser）
② 跑完 CLAUDE.md「四風格一致性檢查」一節的所有指令
③ 390 / 768 / 1024 / 1440px 無水平捲軸
④ 確認頁面無任何外部資源請求
回報每項 PASS/FAIL 與證據，不要順手改檔案。
```

### Prompt B：為勝出風格補齊其餘 18 頁

```text
我們已決定選用 style-{{1-zurich | 2-nordic | 3-soc | 4-continental}} 作為勝出風格。
請依 docs/接手開發_Prompts.md 的「P2」執行——該處已列出 18 個 slug、
文案要求與驗收條件。特別注意：
- pentest.html 是 human-led、scoped engagement with report and retest
- ai-ptaas.html 是 automated、continuous、subscription
  兩者不得混淆（這是採購方最容易問的問題）
- 導覽列與頁尾維持該風格專屬結構，aria-current="page" 設在正確頁面
- 完成後把指向 index.html#offer / #built 的暫代錨點換成實際檔案連結
```

### Prompt C：產生正式版 Astro 網站

```text
請讀取 docs/Volcatech_多風格_Build_Prompts.md（全案唯一事實來源）。
我們選定 style-{{X}} 為勝出風格。請結合「A. 共用基底 Prompt」與「風格 {{X}} 模組」，
在 site/ 目錄初始化全新 Astro 專案（不要改動現有 demo 資料夾），實現
19 個產品/服務頁 × 雙語（EN / ZH-TW）鏡像、3 個總覽頁、GDPR 隱私頁與 Imprint、
sitemap/hreflang，以及 GitHub Actions 自動化部署。
驗收依該檔的【品質底線(驗收)】——不要用 docs/官網建置計畫_Build_Prompt_v3.md 的 §9，
那份已凍結失效。
```

---

## 5. 本地測試

```bash
# 在專案根目錄執行
python3 -m http.server 8000

# 瀏覽器開啟：
# 風格總覽：http://localhost:8000/
# Style 1 (Zurich)：      http://localhost:8000/style-1-zurich/
# Style 2 (Nordic)：      http://localhost:8000/style-2-nordic/
# Style 3 (SOC)：         http://localhost:8000/style-3-soc/
# Style 4 (Continental)： http://localhost:8000/style-4-continental/
```
