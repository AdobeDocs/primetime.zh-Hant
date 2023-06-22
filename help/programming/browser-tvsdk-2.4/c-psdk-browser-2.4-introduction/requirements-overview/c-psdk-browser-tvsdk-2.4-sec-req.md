---
description: 瀏覽器TVSDK有一些需要注意的安全性考量。
title: 安全性考量
exl-id: bc98890a-082a-4e2d-b927-ecb3bd878de9
source-git-commit: 78be1575cc7bd6630a7bf85faa061327e5c414d7
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 安全性考量{#security-considerations}

瀏覽器TVSDK有一些需要注意的安全性考量。

* **AdobeFlash Player**

   * Flash Player不允許存取位於SWF來源網域以外的資料。

      若要允許存取，請在託管資料的伺服器根目錄下，以適當許可權託管跨網域原則檔案。 在瀏覽器TVSDK的Flash遞補模式(Flash Player版本23及更新版本)中，您需要網域的授權Token。 若要產生代號，請聯絡您的Adobe代表。

* **JavaScript**

   * JavaScript遵循相同的原始原則，並防止跨網域邊界存取資源。

      若要允許存取這些資源，Access-Control-Allow-Origin (CORS)標頭必須設定於在播放器以外的原始裝置上託管的資源。 或者，如果使用位元組範圍指定內容，CORS預檢選項要求必須指出來源允許這些要求。

* **瀏覽器和混合式內容**

   * 瀏覽器要求透過安全的來源（例如HTTPS）來託管AES-128加密內容。

      由於大多數瀏覽器不允許混合式內容，因此我們建議將播放器、內容和相關資產（例如金鑰/WebVTT檔案）也託管於安全的Origin上。

      >[!IMPORTANT]
      >
      >從2.4.5版開始，如果播放器是透過HTTPS託管，則瀏覽器TVSDK會在使用MSE技術時將HTTP呼叫轉換為HTTPS。
