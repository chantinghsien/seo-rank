# **SEO 關鍵字排名紀錄工具 (BYOK 模式)**

這是一個專為 SEO 執行人員設計的輕量化、純前端工具。透過 Bring Your Own Key (BYOK) 模式，使用者可以使用自己的 Google API 金鑰來查詢關鍵字排名，並自動將結果記錄到指定的 Google Sheets 試算表中。本工具不經過任何後端伺服器，確保數據隱私與成本控制。

## **專案核心特色**

* 純前端架構：由 HTML、Tailwind CSS 與 JavaScript 組成，可直接部署於 GitHub Pages 或任何靜態網頁空間。  
* 數據隱私保護：所有 API 金鑰與設定僅儲存在使用者的瀏覽器 localStorage 中，不外流至第三方伺服器。  
* 自動化紀錄流程：整合 Google Sheets API，查詢完畢後自動將日期、關鍵字、網址、排名寫入指定試算表。  
* 深度排名查詢：支援 Google Custom Search 分頁抓取功能，最高可查詢至搜尋結果的前 100 名。  
* 響應式介面設計：採用深色主題與現代化 UI 佈局，支援手機與電腦端操作。

## **快速上手指南**

### **1\. Google Cloud 專案設定**

1. 前往 Google Cloud Console。  
2. 建立新專案，並在「API 和服務」中搜尋並啟用以下兩項 API：  
   * Custom Search API  
   * Google Sheets API  
3. 前往「憑證」頁面：  
   * 建立 API 金鑰（用於查詢排名）。  
   * 建立 OAuth 2.0 用戶端 ID（選擇「網頁應用程式」）。  
   * 重要：在 OAuth 的「授權的 JavaScript 來源」填入您部署的網址（例如：https://www.google.com/search?q=https://yourname.github.io）。

### **2\. 搜尋引擎設定 (CX)**

1. 前往 Google Programmable Search Engine 官方網站。  
2. 建立一個新的搜尋引擎。  
3. 在設定中開啟「搜尋整個網路」，並獲取該搜尋引擎的搜尋引擎 ID (CX)。

### **3\. 試算表準備**

1. 建立一個新的 Google Sheet 試算表。  
2. 從網址中複製試算表 ID（位於 /d/ 與 /edit 之間的字串）。

### **4\. 開始使用**

1. 開啟工具網頁，進入「API 設定」分頁。  
2. 填入 API Key、CX、Sheet ID 以及 Client ID。  
3. 點擊「儲存設定」。  
4. 切換至「查詢與紀錄」，輸入目標網址與關鍵字後，點擊「查詢並記錄排名」。  
5. 首次執行時，請依照瀏覽器彈窗指示完成 Google 帳號授權。

## **技術細節**

* 前端框架：Tailwind CSS  
* 授權協議：Google Identity Services (GSI) OAuth 2.0 Implicit Flow  
* API 串接：Fetch API  
* 儲存方案：Browser LocalStorage

## **使用須知與限制**

* API 配額：Google Custom Search API 每日提供 100 次免費查詢額度。  
* 安全性提醒：請確保 OAuth 設定中的「授權的 JavaScript 來源」與實際網址一致，否則授權功能將無法正常運作。  
* 數據同步：本工具預設將資料寫入試算表的第一個工作表 (Sheet1)，欄位順序為日期、關鍵字、網址、排名。

## **授權說明**

本專案採用 MIT 授權協議，歡迎個人或企業自由修改與分發。