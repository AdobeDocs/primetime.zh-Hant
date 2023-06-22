---
title: 概觀
description: 概觀
copied-description: true
exl-id: 7327386b-e796-4fa5-bda4-cacc612a9d1f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 概觀{#overview}

若要向使用者端發行授權，您必須部署Adobe存取授權伺服器。 授權伺服器會使用Adobe® Access™ SDK來執行下列工作：

* 如果支援使用者名稱/密碼驗證，則處理驗證請求。
* 處理授權請求
* 處理取得伺服器版本要求 — 所有伺服器都必須實作這類要求的支援。
* 處理網域註冊要求 — 僅在實作網域伺服器時需要。
* 處理網域取消註冊請求 — 僅在實作網域伺服器時需要。
* 程式同步 — 只有在授權指定同步要求時才需要。

此外，伺服器需要提供商業邏輯來驗證使用者、判斷使用者是否獲得檢視內容的授權，以及選擇性地追蹤授權使用情況。

如需本章所述Java API的詳細資訊，請參閱 *Adobe存取API參考*.
