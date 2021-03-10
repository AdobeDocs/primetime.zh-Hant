---
description: 瀏覽器TVSDK需注意一些安全性考量。
title: 安全性考量
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# 安全注意事項{#security-considerations}

瀏覽器TVSDK需注意一些安全性考量。

* **AdobeFlash Player**

   * Flash Player不允許存取SWF來源網域以外的資料。

      若要允許存取，請在裝載資料之伺服器的根目錄上，以適當的權限來裝載跨網域原則檔案。 在瀏覽器TVSDK(Flash版本23及更新版本)的Flash Player備援模式中，您需要網域的授權Token。 若要產生Token，請連絡您的Adobe代表。

* **JavaScript**

   * JavaScript遵循相同的原始原則，並防止跨網域存取資源。

      若要允許存取這些資源，必須在播放器以外之來源代管的資源上設定「存取控制允許來源」(CORS)標題。 或者，如果內容是透過使用位元組範圍來指定，CORS預備選項要求必須指出來源允許這些要求。

* **瀏覽器和混合內容**

   * 瀏覽器要求AES-128加密內容必須透過安全原始碼（例如HTTPS）代管。

      由於大部分瀏覽器不允許混合內容，因此我們建議播放器、內容和相關資產（例如Key/ WebVTT檔案）也應透過安全原始碼托管。

      >[!IMPORTANT]
      >
      >從2.4.5版開始，如果播放器是透過HTTPS代管，則瀏覽器TVSDK會在使用MSE技術時將HTTP呼叫轉換為HTTPS。

