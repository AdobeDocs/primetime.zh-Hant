---
title: 使用模型演示業務規則
description: 使用模型演示業務規則
copied-description: true
exl-id: 689a0335-55e9-427a-bc27-3a69e37ef0b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 使用模型演示業務規則{#usage-model-demo-business-rules}

當用戶請求許可證時，參考實施伺服器檢查客戶端發送的元資料，以確定內容是否通過使用 `RI_UsageModelDemo` 屬性。 如果是這樣，伺服器應用以下業務規則。

* 如果DRM策略之一需要驗證：

   * 如果請求包含有效的驗證令牌，請在「客戶」資料庫表中搜索用戶的名稱。

      如果找不到用戶的名稱，請完成以下任務：

      * 如果 `Customer.IsSubscriber` 屬性設定為 `true`，需要為 *`Subscription`* 使用模式併發送給用戶。

      * 在中搜索記錄 `CustomerAuthorization` 用戶名和內容ID的資料庫表。

      如果可以找到用戶記錄，請完成以下任務：

      * 如果 `CustomerAuthorization.UsageType` 屬性設定為 `DTO`，為DTO使用模式生成許可證並將其發送給用戶。

      * 如果 `CustomerAuthorization.UsageType` 屬性設定為 `VOD`生成VOD使用模型的許可，併發送給用戶。

      如果所有DRM策略都不允許匿名訪問，請完成以下任務：

      * 如果請求中沒有有效的驗證令牌，則需要返回「需要驗證」錯誤。
      * 否則返回「未授權」錯誤。



* 如果DRM策略之一允許匿名訪問，則生成用於由廣告資助的使用模型的許可並將其發送給用戶。
