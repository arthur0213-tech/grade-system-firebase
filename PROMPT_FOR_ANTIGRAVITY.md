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

## 🚀 Antigravity 執行步驟指南

### 第一步：Git 倉庫初始化與提交 (Git Init & Commit)
請在專案根目錄執行以下指令：
```bash
git init
git add .
git commit -m "feat: 初版發布 - 學生學業成績查詢系統 (支援Firebase Hosting與Firestore)"
```

### 第二步：上傳至 GitHub 倉庫 (Push to GitHub)
1. 若已有新建之 GitHub Repo，請設定遠端並推播：
```bash
git branch -M main
git remote add origin https://github.com/<YOUR_GITHUB_USERNAME>/<YOUR_REPO_NAME>.git
git push -u origin main
```
2. 若使用 GitHub CLI (`gh`)，可直接一鍵建立並推播：
```bash
gh repo create grade-system --public --source=. --remote=origin --push
```

---

### 第三步：連結 Firebase 專案與部署 (Firebase Deploy)

1. **安裝並登入 Firebase CLI**（若環境尚未安裝）：
```bash
npm install -g firebase-tools
firebase login
```

2. **連結專案 ID**：
請在 `.firebaserc` 中將 `YOUR_FIREBASE_PROJECT_ID` 替換為實際的 Firebase 專案 ID，或執行：
```bash
firebase use --add
```
（在清單中選取您的 Firebase 專案，別名設為 `default`）

3. **替換 Firebase 連線金鑰**：
開啟 `public/index.html`，找到第 560 行左右的 `firebaseConfig` 物件，填入您的 Firebase 專案設定資訊：
```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "your-project-id.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project-id.appspot.com",
  messagingSenderId: "123456789...",
  appId: "1:123456789:web:abcdef..."
};
```
*提示：即使尚未填入金鑰，系統亦會自動以本機 LocalStorage 模式完美運作，完全不卡死。*

4. **一鍵部署 Hosting 與 Firestore 安全規則**：
```bash
firebase deploy
```
部署完成後，終端機將會輸出專屬的公開查詢網址（例如：`https://<YOUR_PROJECT_ID>.web.app`）。

---

### 第四步：設定 GitHub Actions 自動持續部署 (CI/CD)
本專案已包含 `.github/workflows/firebase-hosting-merge.yml`。若希望在每次 `git push main` 時自動重新部署，請執行：
```bash
firebase init hosting:github
```
此指令會自動在 GitHub 儲存庫的 Secrets 中產生 `FIREBASE_SERVICE_ACCOUNT_...`，實現全自動發布！

---

## 🔒 預設帳號與測試資料
- **家長查詢登入**：
  - 座號：選取 `01` 號
  - 密碼：預設為身分證末四碼 `5621`
- **教師後台管理員**：
  - 點擊右上角「後台管理」按鈕
  - 預設管理員密碼：`admin888`
  - 可於後台頂端即時更改「班級名稱」（如改為「七年五班」）、即時編輯成績、排定開放時間或批次覆蓋學生名冊。
