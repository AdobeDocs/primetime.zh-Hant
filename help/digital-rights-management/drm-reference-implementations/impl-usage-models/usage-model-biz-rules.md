---
title: 使用模式示範商業規則
description: 使用模式示範商業規則
copied-description: true
exl-id: 689a0335-55e9-427a-bc27-3a69e37ef0b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 使用模式示範商業規則{#usage-model-demo-business-rules}

當使用者請求授權時，Reference Implementation Server會檢查使用者端已傳送的中繼資料，以判斷內容是否已透過以下方式封裝 `RI_UsageModelDemo` 屬性。 如果是這種情況，伺服器會套用以下商業規則。

* 如果其中一個DRM原則需要驗證：

   * 如果請求包含有效的驗證Token，請在Customer資料庫表格中搜尋使用者名稱。

      如果您找不到使用者名稱，請完成下列工作：

      * 如果 `Customer.IsSubscriber` 屬性已設定為 `true`，您需要為產生授權 *`Subscription`* 使用模式，並將其傳送給使用者。

      * 搜尋中的記錄 `CustomerAuthorization` 使用者名稱和內容ID的資料庫表格。

      如果您可以找到使用者的記錄，請完成下列工作：

      * 如果 `CustomerAuthorization.UsageType` 屬性已設定為 `DTO`，為DTO使用模式產生授權，並傳送給使用者。

      * 如果 `CustomerAuthorization.UsageType` 屬性已設定為 `VOD`，產生VOD使用模式的授權並傳送給使用者。

      如果任何DRM原則都不允許匿名存取，請完成下列工作：

      * 如果請求中沒有有效的驗證Token，則需要傳回「需要驗證」錯誤。
      * 否則會傳回「未授權」錯誤。



* 如果其中一個DRM原則允許匿名存取，請為廣告資助的使用模式產生授權，並將其傳送給使用者。
