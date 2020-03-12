---
description: 使用HTTP GET命令與資訊清單伺服器互動。
seo-description: 使用HTTP GET命令與資訊清單伺服器互動。
seo-title: 傳送命令至資訊清單伺服器
title: 傳送命令至資訊清單伺服器
uuid: e9680563-d268-406d-87ce-1521a677e9ec
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 傳送命令至資訊清單伺服器 {#send-a-command-to-the-manifest-server}

使用HTTP GET命令與資訊清單伺服器互動。

1. 傳送使 `HTTP GET` 用下列模式建構的引導URL請求：

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **需要PublisherAssetID** 。 特定內容的發行者唯一ID。

* **需要內容URL** 。 內容M3U8檔案的URL,Base64編碼為在資訊清單伺服器URL中安全。 內容URL必須指向變數的M3U8檔案，即使只有一個位元速率串流亦然。

* **查詢參數** ：部分為必要參數，部分為可選參數。 這些是請求中最多樣的部分。 他們會告訴資訊清單伺服器提出要求的用戶端類型，以及資訊清單伺服器要做什麼。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP與HTTPS要求**

   資訊清單伺服器會使用與用戶端要求相同的HTTP通訊協定來建立URL。 如果播放器發出非安全的HTTP(http)要求，資訊清單伺服器會以http通訊協定傳回資訊清單URL和Auditude追蹤URL。 如果播放器建立安全的HTTP(https)連線，manifest伺服器，則會傳回具有https通訊協定的資訊清單URL和Auditude追蹤URL。

   >[!NOTE]
   >
   >資訊清單伺服器無法變更內容區段(.ts)和第三方追蹤信標的通訊協定（HTTP或HTTPS）。 您必須聯絡內容和第三方廣告供應商，讓他們設定所需的通訊協定。