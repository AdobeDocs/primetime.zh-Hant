---
title: 許可證伺服器概述
description: 許可證伺服器概述
copied-description: true
exl-id: 101d9f63-b9b9-4281-a069-8c66427b34cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概述 {#license-server-overview}

必須先部署Adobe PrimetimeDRM許可證伺服器，然後才能向客戶端頒發許可證。 許可證伺服器使用黃金時段DRM SDK執行多個任務。

要實施許可證伺服器：

* 如果支援用戶名/密碼驗證，則處理驗證請求。
* 處理許可證請求
* 處理獲取伺服器版本請求 — 所有伺服器必須實現對此類請求的支援。
* 處理域註冊請求 — 僅當實施域伺服器時才需要。
* 處理域取消註冊請求 — 僅在實施域伺服器時才需要。
* 進程同步 — 僅當許可證指定同步要求時才需要。

此外，伺服器需要提供業務邏輯來驗證用戶、確定用戶是否有權查看內容，以及可選地跟蹤許可證使用情況。

請參閱 *Adobe PrimetimeDRM API參考* 的子菜單。
