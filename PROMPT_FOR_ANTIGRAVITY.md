# 🤖 給 Antigravity 執行的自動化部署指令與工作流 (Prompt for Antigravity)

請 Antigravity 協助將此學生成績查詢系統專案上傳至 GitHub，並連結部署至 Google Firebase (Firebase Hosting + Cloud Firestore)。

---

## 📋 專案簡介與架構說明
- **專案名稱**：學生學業成績查詢系統與後台管理 (Grade System)
- **前端架構**：單頁式 Web 應用程式 (`public/index.html`)，採用 Tailwind CSS + Chart.js + Firebase Web SDK (v10)。
- **後端與託管**：
  - **Firebase Hosting**：託管 `public/` 靜態網頁，支援全球 CDN 加速與自訂網址。
  - **Cloud Firestore**：儲存學生名冊、各次定期評量成績、開放查詢時間排程、家長查閱日誌與自訂班級名稱。
- **教育規範合規**：系統落實「放假前一日不公布評量成績」之教育法規保護機制，家長端僅呈現個別得分與全班 10 分級距分佈圖（黃色突顯孩子區間），不顯示班級名次、最高最低分或平均等第以維護隱私。

---

## 🔒 預設帳號與測試資料
- **家長查詢登入**：
  - 座號：選取 `01` 號
  - 密碼：預設為身分證末四碼 `5621`（亦可於登入頁點選「快速填入 01 號登入」）
- **教師後台管理員**：
  - 點擊右上角「後台管理」按鈕
  - 預設管理員密碼：`admin888`
