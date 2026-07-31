# CLAUDE.md — Volcatech 官網風格 Demo 專案指示

> 本檔由 Claude Code 自動讀取。接手本專案的任何 AI 助手與開發者都應遵守以下規則。

## 回覆語言

一律以繁體中文回覆;程式碼、指令、專有名詞與技術術語保留原文。

## 這個專案是什麼

沃凱科技(Volcatech)新官網的**風格評選 demo**:**資訊架構與文案完全相同**
(3 條業務板塊 / 19 項服務 / 共用 H1 與所有內文,四風格逐字一致),
**只有導覽的組織方式與視覺呈現依風格而異**,做成 4 個歐洲設計風格供內部評選。
每個風格 2 頁:`index.html`(首頁)+ `sentinelone.html`(產品頁範例)。
另有**第二輪「版型變體」評選** `layout-1`〜`layout-4`:色系與導覽語彙沿用同號 style、
**只換版型框架**,每變體 5 頁(另含 `services.html` / `about.html` / `contact.html`);
「style-N vs layout-N」是唯一變因為版型的對照組。正本:`docs/Volcatech_版型變體_Build_Prompts.md`。
此外根目錄另有**外部 AI 參考組** `Volcatech_Layout_Variants_GPT/`:同一份版型變體規格交給 GPT 產出的實作,
**唯讀參考、不屬本專案維護範圍**——規則見下方專節。

- 目標受眾:歐洲企業的 IT / 資安決策者;語言英文為主(正式版另有繁中 /zh-tw/,架構須可擴充更多語系)
- 新官網將**改版取代**現有 volcatech.com
- 公司事實唯一可信來源:`docs/公司_104.md`(僅可用於服務範圍與願景,**不可**用來填統編/VAT/地址)
- 勝出風格確定後,依 `docs/Volcatech_多風格_Build_Prompts.md` 的「共用基底 + 勝出風格模組」
  產生正式 **Astro** 版(雙語 i18n、19 個產品/服務頁、GDPR 隱私頁、sitemap/hreflang)
- **唯一事實來源(SSOT)**:`docs/Volcatech_多風格_Build_Prompts.md`。
  `docs/官網建置計畫_Build_Prompt_v3.md` 已凍結為 **legacy**(僅供背景脈絡,
  其產品數量、資訊架構、路由、schema、§9 驗收清單皆已失效,勿照做)。

## 硬性規則(所有修改必須遵守)

1. **純靜態、單檔自足**:demo 頁為 HTML + inline CSS(+極少量原生 JS,僅限手機選單/下拉);
   禁止外部 CDN(含 Google Fonts,GDPR)、禁止前端框架、禁止建置步驟。
2. **相對路徑**:所有連結與資源用相對路徑(需相容 GitHub Pages 子路徑 `/repo名稱/`)。
3. **首屏鐵則**:首頁首屏必須有 H1 一句話 + 明列**三條業務板塊**
   (Cloud Infrastructure / Cybersecurity / Managed Services)各附入口連結。
   任何改版不得破壞「3 秒看懂賣什麼(雲端 + 資安 + 託管維運)」。
   - H1 定稿(四風格逐字相同,不得改寫):
     `Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`
   - 副標定稿:`We design and run Google Cloud environments for European organisations, deploy and tune
     EDR and SIEM, and keep both under 24/7 monitoring. One team, one contract, one point of accountability.`
   - 首頁必備第 4 區 **Built by Volcatech**(自研 CE-BAS / AI-PTaaS / SecPurple):
     它是首頁區塊,**不是**第 4 條產品線,**不進頂層導覽**。
4. **不虛構公司事實**:統編、地址、認證(ISO 等)、客戶案例、合作等級一律 `[TODO: 說明]` 佔位,待確認才填。
   **全案只用 `[TODO: 說明]` 一種佔位語法**(不得用 `{{TODO}}`);建置參數用 `[VAR: 名稱]`。
5. **風格隔離**:每個 `style-*` 資料夾有自己的 design tokens(`:root` CSS variables),
   不可跨資料夾混用;調整某風格只改該資料夾。
6. **無障礙與品質**:WCAG 2.2 AA 對比、`:focus-visible`、`prefers-reduced-motion`、
   語意化 HTML、每頁唯一 `<h1>`、RWD(390 / 768 / 1024 / 1440px、無水平捲軸)。
7. **文案**:歐洲 B2B 直述語氣(做什麼、給誰、成果),禁「最先進/領導品牌」等 hype;
   日期用 `30 Jul 2026` 或 ISO 8601、24 小時制、電話 +886 國際格式、不放 LINE。
8. **原廠產品描述必須改寫**,不得複製原廠官網文案;外連原廠網站用 `target="_blank" rel="noopener"`。

## 風格 tokens 速查

| 風格 | bg / ink | accent | 字體(正式版 @fontsource) | 簽名元素 | 導覽列(Nav)結構 |
|---|---|---|---|---|---|
| style-1-zurich | #F7F7F5 / #1A1A1A | #1D4ED8 | Space Grotesk + Inter | 型錄索引碼 + 細網格 hero | 扁平型錄索引:`(C)` / `(E·S·A)` / `(X)` 三個下拉,葉節點帶完整品號 |
| style-2-nordic | #FBFAF7 / #1C2321 | #2E5A4E | Source Serif 4(僅 H1/H2)+ Inter | 目錄式 Hero | 極簡單一 Mega-menu("What We Offer",展開 3 欄 = 6/8/5 項);無頂層 Home |
| style-3-soc | #0E141F / #E9EEF5 | #FFB224(+狀態綠 #3ECF8E 僅圓點) | IBM Plex Sans + Plex Mono | mono 狀態列 + 狀態點 | 維運術語 Platform / Arsenal / Operations;每個下拉首行為白話對照 |
| style-4-continental | #FFFFFF / #14181D | #0F3D8A(+規範紅 #C8102E 僅細線) | Barlow + Inter | 規格書卡片 + 編號章節 | 雙層 header(上層 Imprint/隱私/語言;下層 `§1`–`§3` + Company)+ `Request a proposal` CTA |

各風格「額外禁止事項」與**選單逐字定義**見 `docs/Volcatech_多風格_Build_Prompts.md` §B 對應模組。
版型變體沿用同號風格的 tokens:layout-1(雜誌)=style-1、layout-2(分割 hero)=style-2、
layout-3(Bento)=style-3、layout-4(固定側欄)=style-4;版型模組定義見 `docs/Volcatech_版型變體_Build_Prompts.md` §B。

## 四風格一致性鐵則(評選有效性的前提)

評選要比的是「視覺與導覽體驗」,不是「誰的文案寫得好」。因此:

- **必須逐字相同**:H1、副標、三線區文案與行動連結、Built by Volcatech 三品描述、
  Why Volcatech 三點、Trust 行、CTA band 標題、footer legal block。
- **必須相同**:3 條業務板塊、19 項服務與其群組歸屬與順序、
  section 順序與 `id`(`top` → `offer` → `built` → `why` → `trust` → `vendors` → `contact` → `legal`)。
- **允許差異**:選單組織方式與命名語彙、版面/字體/色彩/間距/簽名元素。
- **刻意變因(僅此三項,已在根 `index.html` 對評選者說明)**:
  style-4 的 header/hero CTA 用 `Request a proposal`(其餘一律 `Contact us`,sentence case);
  style-2 無頂層 `Home`;style-3 的 `Arsenal` 等維運術語。
- 改任一風格的共用文案 → **四風格必須一起改**,並重跑 §驗證方式 的文案一致性檢查。

## 外部 AI 參考組:`Volcatech_Layout_Variants_GPT/`(唯讀,平常不動它)

**是什麼**:把 `docs/版型變體_外部AI_Prompt_Pack.md`(自足式規格)交給 GPT 跑出來的版型變體實作,
2026-07-31 收進本 repo。結構與第二輪相同:4 個變體 × 5 頁,外加它自己的
`index.html` / `README.md` / `HANDOVER.md` / `CLAUDE.md`。用途是對照「同一份規格、不同 AI 實作」的落差。

**平常不需要異動它,也不需要 review 它**——除非使用者明確指名要改這包或要比對它:

1. **不修改**:不改它的 HTML、不改它的文案、不套用本專案的 tokens、不幫它補返回連結、不做無障礙修補。
   它是外部產出的原始樣本,改過就失去對照價值。發現問題只回報,不動手。
2. **不 review**:本檔 §驗證方式 的一致性檢查與品質檢查**不涵蓋這包**——
   那些指令的 glob(`style-*/` 與 `layout-*/`)本來就掃不到它,**不要為了「檢查完整」把它加進去**。
3. **它自帶的文件不適用於本專案**:`Volcatech_Layout_Variants_GPT/CLAUDE.md` 會被 Claude Code
   自動載入,但那是它自己的 scope 說明(只講 `layout-*/`),**本專案的規則一律以根目錄本檔為準**;
   兩者衝突時以本檔為準,也不要去修它那份。它的 README / HANDOVER 同理。
4. **不是評選對象**:第一輪比色系(style-*)、第二輪比版型(layout-*),這包是參考資料,
   不進評選也不進「四風格一致性鐵則」的管轄範圍。根 `index.html` 已標明「參考,不列入評選」。
5. **有交集時的正確做法**:若決定採用它的某個做法,是把做法**移植到本專案的 `layout-*/`**,
   而不是就地改它;若要拿它跟本專案比對,產出的報告放 `docs/reports/`(帶日期),不要落在它資料夾內。
6. **命名不會撞**:它的 `layout-1-magazine-zurich/` 等子資料夾與本專案根目錄的同名資料夾**內容完全獨立**,
   改本專案的 `layout-*/` 不影響它,反之亦然。編輯前先確認路徑是否含 `Volcatech_Layout_Variants_GPT/` 前綴。

## 常見任務怎麼做

- **微調某風格**:只改該資料夾兩個 html 的 `:root` tokens 與相關 CSS;兩頁需同步。
  **各風格導覽結構不同,修改時勿跨風格複製貼上**;若動到共用文案,見上節一致性鐵則。
- **為勝出風格補產品頁**:複製該風格 `sentinelone.html` → 改 `<title>`、meta description、
  eyebrow 索引碼、內容區塊;產品清單(19 項,含代碼、slug 與原廠網址)見
  `docs/Volcatech_多風格_Build_Prompts.md` §A;完成後把該頁在導覽列/頁尾指向
  `index.html#offer` / `#built` 的暫代錨點換成實際檔案連結。
- **新增混搭風格**:建 `style-5-hybrid/`,以指定風格為基底、只替換指定區塊;
  共用文案照抄不得改寫;並在根目錄 `index.html` 總覽加卡片。
- **微調某版型變體(layout-1〜4,已實作)**:規格正本 `docs/Volcatech_版型變體_Build_Prompts.md`
  (§B 該版型模組),挑選背景見 `docs/版型框架挑選指南.md`;只改該 `layout-*/` 資料夾、
  五頁同步;舊 `style-*/` 是版型對照組,一律不動。
  新頁型(services/about/contact)的共用文案正本在版型變體檔 §A2——動一句=四個變體一起動。
- **產生正式 Astro 版**:不要改造本 demo;在新資料夾/新 repo 依
  `docs/Volcatech_多風格_Build_Prompts.md`(基底 + 勝出模組)執行,
  完成後跑該檔【品質底線(驗收)】清單(**不是** v3 的 §9,那份已失效)。

## 檔案放置規約(維持根目錄乾淨)

**專案根 = 本檔所在目錄**(`/Users/shiro/Work/Volcatech_Web/`);CLAUDE.md、README.md 與 docs 內
所有相對路徑皆以此為基準。

| 要放什麼 | 放哪 |
|---|---|
| 規劃書、需求、prompt 集 | `docs/` |
| 一次性腳本、比對報告、體檢輸出 | 臨時 → scratchpad;要保留 → `docs/reports/`(檔名帶日期) |
| 某風格/版型的頁面與資產 | 只在對應 `style-*/` 或 `layout-*/` 內 |
| 勝出風格的正式 Astro 版 | 新資料夾 `site/`,**不改動本 demo** |
| 制度檔(本檔、HANDOVER.md 等)修改前的備份 | `docs/backups/`,檔名加 `.bak-YYYYMMDD`(即全域維護協議所稱「專案備份目錄」的本專案對應) |
| 外部 AI 產出的整包參考實作 | 根目錄獨立資料夾,原樣保留不拆解(現有:`Volcatech_Layout_Variants_GPT/`) |

根目錄只允許:`index.html`、`README.md`、`CLAUDE.md`、`HANDOVER.md`、`.gitignore`、`.nojekyll` 與上表資料夾
(`.vscode/`、`.github/` 除外)。**不要在根目錄新增散檔**;`.DS_Store` 等系統檔已由 `.gitignore` 排除。
外部 AI 參考組是根目錄唯一容許的例外型資料夾(規則見上方專節),新增同類參考包時比照辦理:
整包放根目錄、名稱標明來源、在本檔與 README 的結構圖登記、根 `index.html` 標「參考,不列入評選」。

根目錄文件分工:`README.md` = 對外接手指南(本機預覽與 GitHub Pages 部署步驟的正本、專案結構圖);
`HANDOVER.md` = 進度與交接速查(規格正本仍在 `docs/`);
`.github/copilot-instructions.md` = 本檔硬性規則的濃縮副本(供 GitHub Copilot 使用者)。

**版控範圍**:demo 推到 public repo 供評選瀏覽,`docs/` 已列入 `.gitignore`
(內部建置計畫不對外),因此**頁面內不得連結 `docs/` 內的檔案**,否則線上會是死連結。
`.nojekyll` 用於關閉 GitHub Pages 的 Jekyll 處理,勿刪。

## 驗證方式(改完必做)

> **檢查範圍**:只含根 `index.html`、`style-*/`、`layout-*/`。
> `Volcatech_Layout_Variants_GPT/` 是外部參考組,**不在檢查範圍內**——下列指令的 glob 刻意不涵蓋它,
> 不要為了湊「全站掃過」而把它加進去(理由見上方外部 AI 參考組專節)。

```bash
python3 -m http.server 8000   # 開 http://localhost:8000 逐頁檢查(含 390px 寬)
```

- HTML 標籤配對可用 Python `html.parser` 快速檢查
- 確認頁面無外部資源請求(DevTools Network 只該有本機檔案):
  `grep -nE '<img |<script src|@import|<link ' style-*/*.html layout-*/*.html` 應為空;
  `grep -noE 'https?://[^"]+' style-*/*.html layout-*/*.html` 只該出現原廠 anchor 且同行有 `rel="noopener"`
  (layout-4 每頁有一個 ≤10 行的 inline `<script>` 做手機抽屜,屬規格內;其餘檔案不得有 `<script>`)
- 深色 style-3 特別檢查長文可讀性;對比可用 DevTools 的 contrast checker

### 一致性檢查(改過共用文案後必跑;涵蓋 style-* 與 layout-* 共 8 個首頁)

```bash
# H1 八個首頁逐字相同 → 應輸出 8
grep -Fl 'from one turn-key partner.' style-*/index.html layout-*/index.html | wc -l
# section 順序八檔必須完全一致
for f in style-*/index.html layout-*/index.html; do echo -n "$f: "; \
  grep -o 'id="\(top\|offer\|built\|why\|trust\|vendors\|contact\|legal\)"' "$f" | tr '\n' ' '; echo; done
# CTA 只能有 Contact us 與 Request a proposal(僅 style-4/layout-4);禁 Contact Us
grep -oh 'Contact us\|Request a proposal\|Contact Us' style-*/*.html layout-*/*.html | sort | uniq -c
# 死連結:每檔應只剩語言切換的 1 個(style-4 有雙處切換器故為 2;layout-* 每檔 1)
grep -c 'href="#"' style-*/*.html layout-*/*.html
# 「繁中」每筆同行都要有 lang 屬性 → 下行應輸出 0
grep -h '繁中' style-*/*.html layout-*/*.html | grep -vc 'lang="zh-Hant-TW"'
# 新頁型文案四變體一致(正本:版型變體檔 §A2) → 每行應輸出 4
grep -Fl 'Everything we run, secure and manage.' layout-*/services.html | wc -l
grep -Fl 'One team for cloud, security and operations.' layout-*/about.html | wc -l
grep -Fl 'This demo form is not connected and stores nothing.' layout-*/contact.html | wc -l
```
