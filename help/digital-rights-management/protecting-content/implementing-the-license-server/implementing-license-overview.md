---
title: 授權伺服器概述
description: 授權伺服器概述
copied-description: true
exl-id: 101d9f63-b9b9-4281-a069-8c66427b34cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概觀 {#license-server-overview}

您必須先部署Adobe Primetime DRM授權伺服器，才能向客戶核發授權。 授權伺服器使用Primetime DRM SDK來執行許多工作。

若要實作License Server：

* 如果支援使用者名稱/密碼驗證，則處理驗證請求。
* 處理授權請求
* 處理取得伺服器版本要求 — 所有伺服器都必須實作這類要求的支援。
* 處理網域註冊請求 — 僅在實作網域伺服器時需要。
* 處理網域取消註冊請求 — 僅在實作網域伺服器時需要。
* 處理同步化 — 僅當授權指定同步化要求時才需要。

此外，伺服器需要提供商業邏輯來驗證使用者、判斷使用者是否獲得檢視內容的授權，以及選擇性地追蹤授權使用情況。

另請參閱 *Adobe Primetime DRM API參考* 以取得有關Java API的詳細資訊。
