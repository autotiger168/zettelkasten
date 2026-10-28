# 卡片盒 Zettelkasten — 部署說明

單一檔案 `index.html`，部署在 GitHub Pages；卡片內容在瀏覽器內以 AES-256-GCM 加密後，才同步到你的**私人**資料 repo。

## 架構

| 位置 | 內容 | 公開？ |
|---|---|---|
| `autotiger168/zettelkasten`（網頁 repo） | 只有 `index.html` 程式 | 公開（GitHub Pages） |
| `autotiger168/zettelkasten-data`（資料 repo） | `vault.json`，加密後的亂碼 | **私人** |

密碼不會上傳；GitHub token 也是加密後只存在各台裝置的瀏覽器。

## 一、部署網頁（約 3 分鐘）

1. GitHub → New repository → 名稱 `zettelkasten` → Public → 勾 Add a README → Create
2. Add file → Upload files → 上傳 `index.html` → Commit
3. Settings → Pages → Source 選 `Deploy from a branch`，Branch 選 `main` / `(root)` → Save
4. 約 1 分鐘後網址：`https://autotiger168.github.io/zettelkasten/`

## 二、建立私人資料 repo

1. New repository → 名稱 `zettelkasten-data` → **Private** → 勾 Add a README（repo 不能是空的）→ Create

## 三、建立 token（只開放這個 repo）

1. GitHub 右上頭像 → Settings → Developer settings → Personal access tokens → **Fine-grained tokens** → Generate new token
2. Repository access：Only select repositories → 選 `zettelkasten-data`
3. Permissions → Repository permissions → **Contents：Read and write**
4. Expiration 建議設一年，到期前重新產生
5. 複製 token（只會顯示一次）

## 四、第一次使用

1. 開啟網址 → 「建立新卡片盒」→ 輸入密碼（要和 ThinkingLab、提示詞資料庫共用，就輸入同一組）→ 勾選「放入 MRAM 磁學示範卡」
2. 右上 ⚙ 設定 → GitHub 同步：帳號 `autotiger168`、repo `zettelkasten-data`、貼上 token → 「測試連線」應顯示「私人 repo，可寫入」→「儲存並同步」
3. 之後每次修改，約 2.5 秒後自動上傳，右上角顯示「已同步」

## 五、其他電腦或手機

開啟同一個網址 → 「從 GitHub 載入」→ 填 repo、token、密碼 → 載入並解鎖。之後各裝置會自動合併（以每張卡最後修改時間為準）。

## 卡片包

⚙ 設定 →「卡片包」可一鍵載入預先寫好的主題卡（載入後與自己的卡片一樣加密保存）：

| 卡片包 | 編號 | 張數 |
|---|---|---|
| RRAM | 10–17 | 17 |
| 車用 NVM | 20–26 | 14 |
| 半導體元件物理 | 30–37 | 16 |
| 半導體封裝 | 40–47 | 16 |
| NVM IC 設計 | 50–58 | 15 |

- 重複載入不會產生重複卡片；刪掉後再按「補齊」可以找回
- 若編號和你的卡片衝突，會自動改用新編號並更新 `[[連結]]`
- 卡片包之間互有連結（例如 RRAM ↔ 車用 ↔ IC 設計），也會連到 MRAM 示範卡；沒載入的那一包，連結會顯示為紅色
- 卡片包內容放在公開的網頁 repo（`packs/` 資料夾），屬一般技術知識；你自己寫的卡片仍只存在私人 repo 且加密

## 使用重點

- **卡片類型**：閃念（隨手記，可不編號）→ 文獻（讀書摘要）→ 永久（用自己的話寫的概念）；索引卡是主題入口
- **編號（Folgezettel）**：`1 → 1a → 1a1`，在卡片上按「長出分支」自動編號
- **連結**：背面輸入 `[[` 會跳出選單；寫 `[[2a]]` 或 `[[2a|自訂文字]]`
- **複習**：Leitner 五箱，間隔 1 / 2 / 4 / 8 / 16 天
- **寫作**：選索引卡，依連結順序與分支展開成文章，可下載 .md
- **存成圖片**：卡片詳情 →「🖼 存圖」選正面／背面／正反面，下載 PNG
- **輸出 PDF**：卡片牆「🖨 輸出 PDF」或卡片詳情「這串輸出 PDF」，版面可選 A4 閱讀版（一頁 4 張）、3×5 吋索引卡、A4 雙面剪裁卡（一頁 8 張，背面左右對調）；列印視窗的目的地選「另存為 PDF」
- **文章 PDF**：寫作頁「🖨 輸出 PDF」
- **一鍵備份 PDF**：卡片牆「📄 全部備份 PDF」或 ⚙ 設定 →「一鍵備份 PDF」。內容包括封面統計、目錄、每張卡完整內容（含連結關係、來源、日期）和標籤索引；目錄與連結在 PDF 中可點擊跳轉。PDF 未加密，請妥善保管
- **快捷鍵**：`N` 新卡、`R` 隨機、`/` 搜尋、空白鍵翻面、複習時 `1/2/3` 評分、`Ctrl+Enter` 儲存

## 安全提醒

- **忘記密碼無法救回**，請定期在設定中「匯出加密備份」
- 變更密碼後，其他裝置需用新密碼重新「從 GitHub 載入」
- 閒置 30 分鐘自動上鎖（可在設定調整）
