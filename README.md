# 🎓 學生學業成績查詢系統與後台管理專案包

> 專為國中小導師與學校打造的學生成績線上查詢專區。家長僅能透過座號與身分證末四碼查看個人成績與常態常態組距直方圖，不公開名次與個人等第；教師具備完整管理後台，可自訂班級名稱、隨時排定開放時間（落實放假前夕不公布評量成績之教育法規保護）與即時追蹤查詢日誌。

---

## 📁 資料夾結構與檔案清單

```text
├── public/
│   └── index.html               # 核心網頁應用程式 (支援 Tailwind CSS, Chart.js, Firebase)
├── .github/
│   └── workflows/
│       └── firebase-hosting-merge.yml # GitHub Actions 自動持續部署 (CI/CD)
├── firebase.json                # Firebase Hosting 與 Firestore 設定檔
├── .firebaserc                  # Firebase 專案綁定配置
├── firestore.rules              # Cloud Firestore 資料庫安全規則
├── firestore.indexes.json       # Firestore 索引配置
├── .gitignore                   # Git 忽略配置
├── PROMPT_FOR_ANTIGRAVITY.md    # 提供給 Antigravity AI 代理人的一鍵執行指令文件
└── README.md                    # 本專案完整說明與技術手冊
```

---

## 🌐 線上部署展示 (Firebase Hosting)
- **正式發布網址**：[https://grade-system-103.web.app](https://grade-system-103.web.app)
- **備用網址**：[https://grade-system-103.firebaseapp.com](https://grade-system-103.firebaseapp.com)
- **GitHub 儲存庫**：[https://github.com/arthur0213-tech/grade-system-firebase](https://github.com/arthur0213-tech/grade-system-firebase)

---

## ✨ 核心特色功能

1. **家長身分驗證**：
   - 透過選取「學生座號」並輸入「學生身分證末四碼」進行登入。
   - 支援顯示/隱藏密碼開關與一鍵測試填入功能。

2. **成績與組距呈現（教育部評量指引規範合規）**：
   - 單一評量項目分數卡片。
   - 10 分級距班級組距分佈直方圖（90-100、80-89、70-79、60-69、50-59、<50分）。
   - 貴子弟所在級距以醒目黃金琥珀色標記，其餘同學為靛青色。
   - **嚴格遵循教育隱私規範**：不顯示班級名次、不標記最高分/最低分、不列全班平均及 A/B/C 等第，避免學生相互攀比或產生假期焦慮。

3. **放假前不公布保護排程**：
   - 支援設定各次定期評量之精確開放查詢日期與時間。
   - 系統自動防呆：若開放時間落在週五或假日放假前夕，自動跳出警示標記，建議預約於放假結束後之上課日（如週一上午 08:00）開放。
   - 評量尚未開放時，家長端顯示友善鎖定倒數畫面與教育部教育法規說明。

4. **教師後台管理中心 (預設密碼 `admin888`)**：
   - **班級名稱即時更改**：可由後台頂部隨時修改班級（例如「八年三班」改為「七年一班」），全站抬頭即時連動。
   - **歷次考試總覽與刪除**：總覽歷次上傳成績，具備安全防呆確認彈窗，支援完整刪除或編輯。
   - **線上成績即時編輯**：提供 3 欄式表格（座號、姓名、成績），支援線上直接打字隨改即存。
   - **極速複製貼上錄入**：支援由 Google 試算表或 Excel 直接複製（座號 姓名 成績）並一鍵解析儲存。
   - **學生名冊維護**：隨時替換真實座號、學生姓名與身分證末四碼密碼。
   - **家長查詢紀錄 (稽核日誌)**：自動記錄家長查詢時間（精確至秒）、登入座號、查看項目與使用裝置，並支援一鍵匯出 CSV。

---

## 🛠️ 如何交給 Antigravity 或手動部署？

### 方式一：交給 Antigravity AI Agent
將專案解壓縮後，把 `PROMPT_FOR_ANTIGRAVITY.md` 的內容交給 Antigravity，它將自動為您完成：
1. 本地 Git 提交與推播至 GitHub。
2. 連結至指定的 Firebase 專案。
3. 部署至 Firebase Hosting 與 Firestore。

### 方式二：手動部署至 Firebase
1. 確保已安裝 Node.js 與 Firebase CLI：
   ```bash
   npm install -g firebase-tools
   firebase login
   ```
2. 將 `.firebaserc` 中的專案 ID 替換為您的 Firebase 專案 ID。
3. 在 `public/index.html` 中的 `firebaseConfig` 填入您的 Firebase 網頁 SDK 金鑰。
4. 執行部署指令：
   ```bash
   firebase deploy
   ```
5. 完成後即可獲取專屬網址，分享給全班家長使用！
