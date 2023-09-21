---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 概觀{#overview}

若要發行授權給使用者端，您必須部署Adobe存取授權伺服器。 授權伺服器使用Adobe® Access™ SDK來執行這些工作：

* 如果支援使用者名稱/密碼驗證，則處理驗證請求。
* 處理授權請求
* Process Get Server Version requests — 所有伺服器都必須實作這類要求的支援。
* 處理網域註冊要求 — 只有在實作網域伺服器時才需要。
* 處理網域取消註冊要求 — 只有在實作網域伺服器時才需要。
* 處理同步化 — 只有在授權指定同步化要求時才需要。

此外，伺服器需要提供商業邏輯來驗證使用者、判斷使用者是否有權檢視內容，以及選擇性地追蹤授權使用情況。

如需本章所述Java API的詳細資訊，請參閱 *Adobe存取API參考*.
