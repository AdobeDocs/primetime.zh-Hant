---
description: 瀏覽器TVSDK需注意一些安全性考量事項。
title: 安全性考量事項
exl-id: bc98890a-082a-4e2d-b927-ecb3bd878de9
source-git-commit: 78be1575cc7bd6630a7bf85faa061327e5c414d7
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 安全性考量事項{#security-considerations}

瀏覽器TVSDK需注意一些安全性考量事項。

* **AdobeFlash Player**

   * Flash Player不允許存取駐留在SWF源自的域之外的資料。

      要允許訪問，請在承載資料的伺服器的根目錄中以適當的權限托管跨域策略檔案。 在FlashTVSDK(Flash Player23版及更新版本)的備援模式中，您需要網域的授權Token。 若要產生代號，請連絡您的Adobe代表。

* **JavaScript**

   * JavaScript會遵循相同的原始政策，並防止跨網域界限存取資源。

      若要允許存取這些資源，必須在托管於播放器以外之原點的資源上，設定Access-Control-Allow-Origin(CORS)標題。 或者，如果內容是透過位元組範圍指定，則CORS預檢選項要求必須指出來源允許這些要求。

* **瀏覽器與混合內容**

   * 瀏覽器要求透過安全來源（例如HTTPS）托管AES-128加密內容。

      由於大部分的瀏覽器不允許混合內容，因此我們建議播放器、內容和相關資產（例如Key/ WebVTT檔案）也透過安全原始碼托管。

      >[!IMPORTANT]
      >
      >從2.4.5版開始，如果播放器是透過HTTPS托管，則瀏覽器TVSDK會在使用MSE技術時，將HTTP呼叫轉換為HTTPS。
