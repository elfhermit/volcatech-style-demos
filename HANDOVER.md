# Volcatech 官網風格 Demo 接手指引 (Handover)

> **最後更新**：2026-08-03
> **本檔定位**：進度速查與接手指令集。
> **規格正本是 `docs/Volcatech_多風格_Build_Prompts.md`**——本檔與它衝突時，一律以它為準。
> 唯一例外：該檔 §B 的 style-3 選單定義（`Platform / Arsenal / Operations`）是**評選期歷史**，
> 0731 會後現行選單以 `style-3-soc/` 頁面為準（見下方 §2）。
> **例外資料夾**：`archive/` 是已凍結的評選歷史（含外部 AI 參考組
> `archive/Volcatech_Layout_Variants_GPT/`，唯讀、不異動也不 review，
> 規則見 `CLAUDE.md` 的「外部 AI 參考組」專節）；本檔所有任務與檢查指令皆不涵蓋它。

---

## 1. 目前狀態

**2026-07-31 內部評選已結束**：勝出組合＝**Style 3（SOC Console 深色色系）× 原版直落版型**，
色系凍結。現行維護對象只有 `style-3-soc/`（`index.html`＝Nav A、`index-nav-b.html`＝Nav B、
`sentinelone.html`，共 3 頁）；落選的 3 個風格、4 個版型變體與 GPT 參考包已全部移入
`archive/`（凍結），舊評選總覽為 `archive/index.html`，根 `index.html` 重寫為 Demo hub。

### 定調的資訊架構（沿用不變）

- **3 條業務板塊**：`Cloud Infrastructure` / `Cybersecurity` / `Managed Services`
- **19 項服務**（清單與 slug 見規格正本 §A）：Cloud 6 + Cybersecurity 8 + Managed 5
- 自研 **CE-BAS / AI-PTaaS / SecPurple** 屬 Cybersecurity 底下的第三個群組，
  但首頁另有專屬的 **Built by Volcatech** 區塊——它不是第 4 條產品線，**不進頂層導覽**
- H1 逐字定稿不變：`Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`
- **section 順序不變**：`top` → `offer` → `built` → `why` → `trust` → `vendors` → `contact` → `legal`

### 0731 會後完成的事

1. **選單分類改名**：`Platform / Arsenal / Operations` → `Google Cloud / CyberSecurity / Services`
   （`CyberSecurity` 駝峰是會議指定的刻意寫法）。每個下拉第一行仍是 mono 白話對照。
   `Google Cloud` 下拉改為 **GCP 產品樹 6 組 18 項**（Compute / Storage / Analytics /
   Serverless / Databases / AI）；`CyberSecurity` 維持原 8 項（EDR / SIEM / Built in-house
   三組）；`Services` 維持原 5 項。
2. **選單雙變體**：`index.html`＝Nav A（單層下拉、mono 小標分組）；`index-nav-b.html`＝Nav B
   （分組升級為第二層 flyout，hover / `:focus-within` 展開）；`sentinelone.html` 用 Nav A。
   兩首頁自 `<main>` 起**逐字節相同**（新一致性鐵則）。
3. **首頁 hero 文案（H1／副標／CTA）改置中**。
4. **歸檔**：style-1／2／4、layout 四個變體、GPT 參考包 → `archive/`；
   補建先前文件宣稱有但實際缺失的 `.nojekyll`。GitHub Pages 部署方式不變，
   `style-3-soc/` 線上路徑不變，被歸檔頁面的網址前多一層 `/archive/`。

（第一、二輪評選期間的完成事項——3 板塊重構、19 項服務擴充、四風格 Top Menu 差異化、
歐規頁尾、無障礙修正、文件收斂等——紀錄已隨頁面歸檔，詳見 git 歷史與 `archive/`。）

---

## 2. 現行導覽結構速查（style-3-soc）

> 兩變體的選單分類與各下拉內容**完全相同**，差別只在「分組的呈現層級」。

| 變體 | 檔案 | 結構 |
|---|---|---|
| **Nav A（單層下拉）** | `index.html`、`sentinelone.html` | `● VOLCATECH` \| `Home` \| `Google Cloud ▾` \| `CyberSecurity ▾` \| `Services ▾` \| `About` \| `[Contact us]` \| `EN 繁中`；下拉內以 mono 小標分組 |
| **Nav B（二層 flyout）** | `index-nav-b.html` | 頂層同 Nav A；下拉內的分組升級為第二層 flyout（hover / `:focus-within` 展開） |

各下拉內容（首行皆為 mono 白話對照）：

- `Google Cloud`：GCP 產品樹 6 組 18 項（Compute / Storage / Analytics / Serverless / Databases / AI）
- `CyberSecurity`：8 項（EDR / SIEM / Built in-house 三組）
- `Services`：5 項

舊風格與版型（Style 1／2／4、Layout 1–4）的導覽結構已隨頁面**歸檔至 `archive/`**（凍結），
逐字定義見規格正本 §B（評選歷史，僅供回顧）。

### 現行注意事項（改 style-3-soc 前必讀）

1. 選單分類 `CyberSecurity` 的**駝峰寫法是 0731 會議指定的刻意寫法**，不要「修正」成
   Cybersecurity（僅限選單分類名；H1 等內文仍為定稿原文的正常拼寫）。
2. **兩首頁變體自 `<main>` 起逐字節相同**（一致性鐵則）：改任何 `<main>` 之後的內容，
   兩檔必須同步，改完用 diff 驗證：
   `diff <(sed -n '/<main/,$p' style-3-soc/index.html) <(sed -n '/<main/,$p' style-3-soc/index-nav-b.html)`
3. `sentinelone.html` 用 Nav A；若最終定稿選 Nav B，屆時需同步它的 header。

---

## 3. 待辦（Roadmap）

- [x] **任務 1：內部評選——已完成（2026-07-31）**：勝出組合＝Style 3（SOC Console 色系）×
      原版直落版型，色系凍結。會後已完成：hero 文案置中、選單分類改名
      （`Google Cloud / CyberSecurity / Services`）＋ GCP 產品樹、選單雙變體（Nav A／Nav B）。
      落選風格與版型已歸檔至 `archive/`。會議紀錄見 `docs/meeting_0731.md`。
- [ ] **任務 1d（進行中）：選單變體擇一定稿**：比對 `index.html`（Nav A）與
      `index-nav-b.html`（Nav B），擇一後併回單一 `index.html` 並同步 `sentinelone.html` 的 header。
- [ ] **任務 2：補齊其餘 18 個產品/服務頁**（目前僅 `sentinelone.html`）。用下方 Prompt B。
- [ ] **待辦：部分內容頁補詳細資訊**（範圍待使用者指定）。
- [ ] **任務 3：向公司取得法定資訊並替換 `[TODO`**：
      註冊地址、統一編號、VAT／稅籍編號、對外聯絡 Email、電話（+886 國際格式）。
      另外 **ISO 27001 等認證狀態**與 **Google Cloud 合作等級**未經確認**絕不可寫上去**。
      注意：`docs/公司_104.md` 是公司自述，**不是法定登記資料**，不能拿來填統編或地址。
- [x] **任務 1b：版型變體 demo（第二輪評選）——已實作（2026-07-31）**，評選結束後已隨
      落選內容歸檔至 `archive/`（凍結）。規格正本 `docs/Volcatech_版型變體_Build_Prompts.md`、
      挑選背景 `docs/版型框架挑選指南.md` 保留為評選歷史。
- [x] **任務 1c：外部 AI 參考組收錄——已完成（2026-07-31）**，現位於
      `archive/Volcatech_Layout_Variants_GPT/`，**維持唯讀：不異動、不 review、不納入檢查**；
      規則正本在 `CLAUDE.md`「外部 AI 參考組」專節。
- [ ] **任務 4：建置正式版 Astro 專案**於 `site/`。用下方 Prompt C。
- [ ] （未來）繁體中文版與更多語系：i18n 架構已要求語系清單集中於單一陣列，新增語系不需改元件。

---

## 4. 可直接複製給下一位 AI 的 Prompts

### Prompt A：預覽與驗收檢查

```text
請讀取根目錄的 HANDOVER.md 與 CLAUDE.md。
用 python3 -m http.server 8000 啟動本機伺服器，對 style-3-soc 的三頁
（index.html、index-nav-b.html、sentinelone.html）做檢查：
① HTML 標籤配對（python html.parser）
② 兩首頁變體自 <main> 起逐字節相同（diff 驗證）
③ 390 / 768 / 1024 / 1440px 無水平捲軸（Nav B 的二層 flyout 特別看窄幅）
④ 確認頁面無任何外部資源請求
檢查範圍不含 archive/（已凍結的評選歷史，不 review）。
回報每項 PASS/FAIL 與證據，不要順手改檔案。
```

### Prompt B：為勝出風格補齊其餘 18 頁

```text
勝出風格已定為 style-3-soc（2026-07-31 評選）。
請依 docs/接手開發_Prompts.md 的「P2」執行——該處已列出 18 個 slug、
文案要求與驗收條件。特別注意：
- pentest.html 是 human-led、scoped engagement with report and retest
- ai-ptaas.html 是 automated、continuous、subscription
  兩者不得混淆（這是採購方最容易問的問題）
- 導覽列與頁尾維持 style-3-soc 現行結構（Google Cloud / CyberSecurity / Services，
  用 Nav A；CyberSecurity 駝峰是刻意寫法），aria-current="page" 設在正確頁面
- 完成後把指向 index.html#offer / #built 的暫代錨點換成實際檔案連結
```

### Prompt C：產生正式版 Astro 網站

```text
請讀取 docs/Volcatech_多風格_Build_Prompts.md（全案唯一事實來源）。
勝出風格為 Style 3（SOC Console，2026-07-31 評選定案）。
請結合「A. 共用基底 Prompt」與「風格 3 模組」，
在 site/ 目錄初始化全新 Astro 專案（不要改動現有 demo 資料夾），實現
19 個產品/服務頁 × 雙語（EN / ZH-TW）鏡像、3 個總覽頁、GDPR 隱私頁與 Imprint、
sitemap/hreflang，以及 GitHub Actions 自動化部署。
注意：該檔 §B 風格 3 模組的選單定義（Platform / Arsenal / Operations）是評選期歷史，
0731 會後選單分類已改為 Google Cloud / CyberSecurity / Services（含 GCP 產品樹），
一律以 style-3-soc/ 現行頁面為準。
驗收依該檔的【品質底線(驗收)】——不要用 docs/官網建置計畫_Build_Prompt_v3.md 的 §9，
那份已凍結失效。
```

---

## 5. 本地測試

```bash
# 在專案根目錄執行
python3 -m http.server 8000

# 瀏覽器開啟：
# Demo hub：                http://localhost:8000/
# 首頁 Nav A（單層下拉）：  http://localhost:8000/style-3-soc/index.html
# 首頁 Nav B（二層 flyout）：http://localhost:8000/style-3-soc/index-nav-b.html
# 產品頁範例：              http://localhost:8000/style-3-soc/sentinelone.html
# 舊評選總覽（已凍結）：    http://localhost:8000/archive/index.html
```
