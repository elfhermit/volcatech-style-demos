# 字體授權（`lab/restyle-0812/fonts/`）

四個檔全部是 **SIL Open Font License 1.1**，允許自架、嵌入與再散布。
一律**自架**（`@font-face` 指向本資料夾），零外部請求——禁 CDN 是本專案的 GDPR 前提。

| 檔案 | 字體 | 來源 | 授權 | 取得日 |
|---|---|---|---|---|
| `inter-latin.woff2` | Inter（可變，400–600 皆涵蓋） | Google Fonts API，latin 分片 | SIL OFL 1.1 · [rsms/inter](https://github.com/rsms/inter) | 2026-08-12 |
| `source-code-pro-latin.woff2` | Source Code Pro（可變） | Google Fonts API，latin 分片 | SIL OFL 1.1 · [adobe-fonts/source-code-pro](https://github.com/adobe-fonts/source-code-pro) | 2026-08-12 |
| `geist-latin.woff2` | Geist（可變） | jsDelivr `npm/geist@1.7.2` | SIL OFL 1.1 · [vercel/geist-font](https://github.com/vercel/geist-font) | 2026-08-12 |
| `geist-mono-latin.woff2` | Geist Mono（可變） | 同上 | SIL OFL 1.1 · [vercel/geist-font](https://github.com/vercel/geist-font) | 2026-08-12 |

共 211 KB。

## 為什麼是這四個

提案 A 照 Supabase、提案 B 照 Harness.io。

- **Supabase 的主字體 Circular 是商業訂閱字體，不能自架**（refero 調查已標明衝突）。
  **Inter 是 Circular 的標準開源替代**——同為幾何無襯線、x-height 相近，是業界慣用的代打。
  等寬則直接用 Supabase 自己在用的 Source Code Pro（本身就是 OFL）。
- **Harness 的 Geist ＋ Calsans 皆開源**。Geist 與 Geist Mono 直接自架；
  **Calsans 只用在 Harness 的展示標題，本提案未採用**——它與 Geist 的字重階梯搭起來
  會多一個變因，而本輪已經在比配色與版型了。

## 只取 latin 分片

四個檔都只涵蓋 latin（`U+0000-00FF` 那一段）。頁面主體是英文，這樣每個檔壓在 70KB 以內。

⚠ **中文不在這些字體裡。**頁面上唯一的中文是語言切換的「繁中」二字，它會沿著
`font-family` 往下 fallback 到系統字型——這是刻意的，不是漏掉。真要自架 CJK 分片，
單一字重就是數 MB 起跳，且踩過坑（全域教訓簿 2026-07-14：Google Fonts 的 `download:true`
根本不抓 CJK 分片，會讓中文 fallback 成簡體字型）。

## 這些檔會進版控

`lab/` 不在 `.gitignore` 裡，所以這 211KB 會推上 GitHub。這是本 repo 第一次放二進位資產——
若最終不採用這兩個提案，連同 `lab/restyle-0812/` 整個刪掉即可。
