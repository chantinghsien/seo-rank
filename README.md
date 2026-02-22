# **🚀 SEO 排名追蹤工具**

這是一個純前端的網頁應用程式，可讓您透過輸入關鍵字與目標網址，自動使用 SerpApi 抓取 Google 前 100 名的搜尋結果，找出該網址的排名，並一鍵將紀錄（日期、關鍵字、網址、排名、標題）儲存到您私人的 Google Sheets 中。

## **✨ 特色**

* **純前端設計**：無須架設後端伺服器，直接透過 index.html 即可運行。  
* **BYOK (Bring Your Own Key)**：金鑰僅存於瀏覽器 localStorage，確保資料安全。  
* **無縫整合**：直接繞過 CORS 請求 SerpApi，並使用最新的 Google Identity Services 進行授權寫入試算表。

## **🛠️ 事前準備與金鑰取得教學**

在使用本工具之前，您需要準備三項資訊：

### **1\. 取得 SerpApi Key**

1. 前往 [SerpApi 官方網站](https://serpapi.com/) 並註冊免費帳號。  
2. 免費帳號每個月提供 100 次的免費搜尋額度。  
3. 登入後，進入 Dashboard，您會看到 **Your Private API Key**。將這串英數字複製下來。

### **2\. 建立 Google Sheet 並取得 ID**

1. 前往 [Google 試算表](https://docs.google.com/spreadsheets/) 建立一個新的空白試算表。  
2. 為了方便閱讀，您可以先在第一列 (A1\~E1) 寫上標題：日期 | 關鍵字 | 目標網址 | 排名 | 網頁標題。  
3. 觀察瀏覽器上方的網址列，網址結構如下：  
   https://docs.google.com/spreadsheets/d/【這是一長串字母與數字的\_Sheet\_ID】/edit  
4. 複製 d/ 到 /edit 之間的那串字元，這就是 **Google Sheet ID**。

### **3\. 取得 Google OAuth Client ID (最重要的一步)**

為了讓前端可以直接請求寫入您的試算表，您需要開啟 Google Cloud 的 API 權限：

1. 前往 [Google Cloud Console](https://console.cloud.google.com/)。  
2. 點擊左上角建立一個新的專案（例如："SEO Tracker"）。  
3. 進入 **「API 和服務」 \> 「程式庫」**，搜尋 Google Sheets API 並點擊 **啟用 (Enable)**。  
4. 進入 **「API 和服務」 \> 「OAuth 同意畫面」**：  
   * User Type 選擇「外部 (External)」，點擊建立。  
   * 填寫必填的「應用程式名稱」、「使用者支援電子郵件」與底下的「開發人員聯絡資訊」。  
   * 直接按儲存並繼續，直到完成（不需要發布，保持在測試狀態即可，並將您的 Google 帳號加入「測試使用者 (Test users)」中）。  
5. 進入 **「API 和服務」 \> 「憑證」**：  
   * 點擊上方「建立憑證」\>「OAuth 用戶端 ID」。  
   * 應用程式類型選擇 **「網頁應用程式 (Web application)」**。  
   * 在「已授權的 JavaScript 來源」中，**必須加入您的網站網址**。  
     * 如果您使用 GitHub Pages 部署，請輸入 https://您的帳號.github.io  
     * 如果您在本地測試，請輸入 http://localhost 或 http://127.0.0.1 加上您的 Port 號。  
   * 點擊建立後，您將會得到一串 **用戶端 ID (Client ID)**，請複製它。

## **🚀 部署與使用方法**

### **部署至 GitHub Pages**

1. 在 GitHub 建立一個新的公開 (Public) 儲存庫。  
2. 將本專案產生的 index.html 上傳至該儲存庫。  
3. 進入儲存庫的 **Settings \> Pages**，將 Source 選擇為 main 分支並儲存。  
4. 幾分鐘後，您的專案就會在 https://\<您的帳號\>.github.io/\<儲存庫名稱\>/ 上線。

### **如何使用**

1. 打開上線的網頁。  
2. 於左側「API 設定」區塊，依序填入：  
   * **SerpApi Key**  
   * **Google Client ID**  
   * **Google Sheet ID**  
3. 點擊 **「儲存設定」**（資料會存在您的瀏覽器，下次打開自動載入）。  
4. 在右側輸入您想查詢的 **目標網址** (例: shopee.tw) 與 **目標關鍵字** (例: 水壺)。  
5. 點擊 **「查詢並記錄至 Google Sheets」**。  
6. 系統會先呼叫 SerpApi 取得排名，完成後會彈出 Google 授權視窗。  
7. 登入您的 Google 帳號並同意授予編輯試算表的權限，資料就會成功寫入！

**注意事項**：免費版的 corsproxy.io 有時會受到流量限制，如果發現卡在 SerpApi 查詢，通常是 Proxy 端的問題。若需用於正式商用，建議自行架設簡單的 Node.js 轉發伺服器。