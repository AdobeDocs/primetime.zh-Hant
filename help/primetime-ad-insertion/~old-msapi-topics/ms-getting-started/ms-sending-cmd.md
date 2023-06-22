---
description: 使用HTTPGET命令與資訊清單伺服器互動。
title: 傳送命令至資訊清單伺服器
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 傳送命令至資訊清單伺服器 {#send-a-command-to-the-manifest-server}

使用HTTPGET命令與資訊清單伺服器互動。

1. 傳送 `HTTP GET` 要求使用下列模式建構的啟動程式URL：

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **PublisherAssetID** 必填。 特定內容的發行者唯一ID。

* **內容URL** 必填。 內容M3U8檔案的URL，在資訊清單伺服器URL中編碼為安全的Base64。 內容URL必須指向變體M3U8檔案，即使只有一個位元速率資料流亦然。

* **查詢引數** 部分為必要專案，部分為選用專案。 這些是請求中最具多樣性的部分。 它們告訴資訊清單伺服器哪個使用者端正在提出要求，以及它想要資訊清單伺服器做什麼。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP與HTTPS要求**

   資訊清單伺服器會使用使用者端要求的相同HTTP通訊協定來建立URL。 如果播放器提出非安全HTTP (http)要求，資訊清單伺服器會傳回資訊清單URL和使用http通訊協定的稽核追蹤URL。 如果播放器透過安全HTTP (https)連線、資訊清單伺服器，會傳回資訊清單URL和使用https通訊協定的稽核追蹤URL。

   >[!NOTE]
   >
   >資訊清單伺服器無法變更內容區段(.ts)和第三方追蹤信標的通訊協定（HTTP或HTTPS）。 您必須連絡內容與第三方廣告提供者，讓他們設定所需的通訊協定。