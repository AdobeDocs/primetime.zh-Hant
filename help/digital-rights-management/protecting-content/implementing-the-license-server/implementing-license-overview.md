---
title: 授權伺服器概述
description: 授權伺服器概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概觀 {#license-server-overview}

您必須先部署Adobe Primetime DRM授權伺服器，才能向使用者端核發授權。 許可證伺服器使用Primetime DRM SDK來執行許多工作。

若要實作License Server：

* 如果支援使用者名稱/密碼驗證，則處理驗證請求。
* 處理授權請求
* 處理取得伺服器版本要求 — 所有伺服器都必須實作這類要求的支援。
* 處理網域註冊要求 — 只有在實作網域伺服器時才需要。
* 處理網域取消註冊要求 — 只有在實作網域伺服器時才需要。
* 處理同步化 — 只有在授權指定「同步化」要求時才需要。

此外，伺服器需要提供商業邏輯來驗證使用者、判斷使用者是否有權檢視內容，以及選擇性地追蹤授權使用情況。

另請參閱 *Adobe Primetime DRM API參考* 以取得有關Java API的詳細資料。
