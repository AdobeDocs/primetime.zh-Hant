---
description: 使用HTTPGET命令與manifest伺服器互動。
title: 傳送命令至資訊清單伺服器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 將命令發送到Manifest伺服器{#send-a-command-to-the-manifest-server}

使用HTTPGET命令與manifest伺服器互動。

1. 傳送`HTTP GET`請求，請求使用下列模式建構的引導URL:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **需** 要PublisherAssetIDR。特定內容的發行者唯一ID。

* **需要** 內容URLRred。內容M3U8檔案的URL,Base64編碼為在資訊清單伺服器URL中安全。 內容URL必須指向變數的M3U8檔案，即使只有一個位元速率串流亦然。

* **查詢** 參數有些是必需的，有些是可選的。這些是請求中最多樣的部分。 他們會告訴資訊清單伺服器提出要求的用戶端類型，以及資訊清單伺服器要做什麼。

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