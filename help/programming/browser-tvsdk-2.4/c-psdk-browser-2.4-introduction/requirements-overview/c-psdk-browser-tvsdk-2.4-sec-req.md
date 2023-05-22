---
description: 對於瀏覽器TVSDK，需要注意一些安全注意事項。
title: 安全考慮事項
exl-id: bc98890a-082a-4e2d-b927-ecb3bd878de9
source-git-commit: 78be1575cc7bd6630a7bf85faa061327e5c414d7
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 安全考慮事項{#security-considerations}

對於瀏覽器TVSDK，需要注意一些安全注意事項。

* **AdobeFlash Player**

   * Flash Player不允許訪問駐留在SWF發源的域之外的資料。

      要允許訪問，請在承載資料的伺服器的根目錄處托管具有適當權限的跨域策略檔案。 在FlashTVSDK(Flash Player版本23及更高版本)的回退模式下，您需要域的授權令牌。 要生成令牌，請與Adobe代表聯繫。

* **JavaScript**

   * JavaScript遵循相同的源策略，並防止跨域邊界訪問資源。

      要允許訪問這些資源，必須在承載於播放器以外的源的資源上設定訪問控制允許來源(CORS)標頭。 或者，如果內容是使用位元組範圍指定的，則CORS飛行前選項請求必須指明這些請求是源允許的。

* **瀏覽器和混合內容**

   * 瀏覽器要求AES-128加密內容通過安全原點（例如HTTPS）托管。

      由於大多數瀏覽器不允許混合內容，因此我們建議播放器、內容和相關資產（如Key/ WebVTT檔案）也通過安全源托管。

      >[!IMPORTANT]
      >
      >從2.4.5版開始，如果播放器是通過HTTPS承載的，則當使用MSE技術時，Browser TVSDK會將HTTP調用轉換為HTTPS。
