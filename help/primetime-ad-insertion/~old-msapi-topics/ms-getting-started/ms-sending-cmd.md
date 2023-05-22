---
description: 使用HTTPGET命令與清單伺服器進行交互。
title: 向清單伺服器發送命令
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 向清單伺服器發送命令 {#send-a-command-to-the-manifest-server}

使用HTTPGET命令與清單伺服器進行交互。

1. 發送 `HTTP GET` 使用以下模式構建的引導URL請求：

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **發佈者資產ID** 必需。 Publisher特定內容的唯一ID。

* **內容URL** 必需。 內容M3U8檔案的URL,Base64編碼為在清單伺服器URL內安全。 內容URL必須指向變型的M3U8檔案，即使只有一個比特率流。

* **查詢參數** 有些是必需的，有些是可選的。 這些是請求中最多樣的部分。 它們會告訴清單伺服器發出請求的客戶機類型，以及它希望清單伺服器執行什麼操作。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP與HTTPS請求**

   清單伺服器使用客戶端請求的相同HTTP協定建立URL。 如果播放器發出非安全HTTP(http)請求，則清單伺服器返回具有http協定的清單URL和審核跟蹤URL。 如果播放器建立了安全的HTTP(https)連接，清單伺服器，則它返回具有https協定的清單URL和審核跟蹤URL。

   >[!NOTE]
   >
   >清單伺服器無法更改內容段(.ts)和第三方跟蹤信標的協定（HTTP或HTTPS）。 您必須聯繫內容和第三方廣告提供商，讓他們配置所需的協定。