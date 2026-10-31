# 台股／美股曝險計算器

純前端響應式網頁，無需安裝、API Key、Node.js 或付費服務。可透過 GitHub Pages 免費部署公開靜態網站。

## 本機使用

將 `index.html`、`style.css`、`app.js` 放在同一資料夾，直接使用瀏覽器開啟 `index.html` 即可。亦可使用 Python `python -m http.server 8000` 後瀏覽 `http://localhost:8000`。

## GitHub Pages 部署

1. 登入 GitHub，點選 **New repository**，名稱輸入 `tw-exposure-calculator`，選擇 **Public**，建立儲存庫。
2. 選擇 **Add file → Upload files**，上傳 `index.html`、`style.css`、`app.js`、`README.md`（**請上傳檔案本身，勿放在子資料夾**），點選 **Commit changes**。
3. 進入儲存庫 **Settings → Pages**。
4. 在 **Build and deployment** 的 **Source** 選 **Deploy from a branch**，Branch 選 `main`，Folder 選 `/(root)`，點 **Save**。
5. 等待 GitHub Pages 完成部署，開啟 `https://<你的GitHub帳號>.github.io/tw-exposure-calculator/`。

> 若你使用的帳號是 `sam8109140601-droid`，預期網址是 `https://sam8109140601-droid.github.io/tw-exposure-calculator/`，但必須先完成建立儲存庫及 Pages 設定，網址才會生效。

## 計算定義

- 淨資產 = 總資產 − 負債。
- 投資市值 = 各部位市值 × 幣別匯率（台股 1、美股輸入的 USD/TWD）。
- 有效曝險 = Σ（部位市值 × 匯率 × 槓桿倍數）。
- 曝險倍數 = 有效曝險 ÷（淨資產 − 可選扣除的預備金）。若分母 ≤ 0，顯示無法計算。
- 情境投資損益 ≈ 有效曝險 × 假設標的市場漲跌幅。

**重要：** 總資產必須包含所有投資部位、現金等資產；若使用借款投資，借款形成的資產已包含在總資產，不要再將借款額加到總資產。台股正2、市值與其他 ETF 部位請勿重複輸入。槓桿 ETF 的實際長期報酬受到每日重設、波動損耗、追蹤誤差與費用影響，並不保證等於標的累積報酬乘以 2。模型假設各標的同幅變動，忽略匯率變動與稅費。美元匯率為手動輸入，沒有即時行情。

## 資料安全

資料儲存在瀏覽器 `localStorage`，不會自動同步至其他裝置。請定期匯出 JSON 備份；匯入會覆蓋當前資料。公開 GitHub 儲存庫僅存放程式碼，**不要上傳個人 JSON 備份或實際帳戶資料**。

## 檔案

- `index.html`：介面結構
- `style.css`：響應式設計
- `app.js`：計算、持股、儲存與備份
- `README.md`：使用與部署說明
