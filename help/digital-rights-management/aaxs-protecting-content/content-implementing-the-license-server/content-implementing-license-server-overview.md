---
title: 概述
description: 概述
copied-description: true
exl-id: 7327386b-e796-4fa5-bda4-cacc612a9d1f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 概述{#overview}

要向客戶端頒發許可證，必須部署Adobe訪問許可證伺服器。 許可證伺服器使用Adobe® Access™ SDK執行以下任務：

* 如果支援用戶名/密碼驗證，則處理驗證請求。
* 處理許可證請求
* 進程獲取伺服器版本請求 — 所有伺服器必須實現對此類請求的支援。
* 處理域註冊請求 — 僅當實施域伺服器時才需要。
* 處理域取消註冊請求 — 僅當實施域伺服器時才需要。
* 進程同步 — 僅當許可證指定同步要求時才需要。

此外，伺服器需要提供業務邏輯來驗證用戶、確定用戶是否有權查看內容，以及可選地跟蹤許可證使用情況。

有關本章中討論的Java API的詳細資訊，請參見 *Adobe訪問API參考*。
