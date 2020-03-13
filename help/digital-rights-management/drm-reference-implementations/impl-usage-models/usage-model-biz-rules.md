---
description: 'null'
seo-description: 'null'
seo-title: 使用模式示範業務規則
title: 使用模式示範業務規則
uuid: c55f85be-5ecb-4a78-b47d-7001ec207d3a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用模式示範業務規則{#usage-model-demo-business-rules}

當使用者要求授權時，Reference Implementation伺服器會檢查用戶端所傳送的中繼資料，以判斷內容是否是使用屬性封裝 `RI_UsageModelDemo` 的。 如果是，則伺服器應用以下業務規則。

* 如果DRM策略之一需要驗證：

   * 如果請求包含有效的驗證Token，請在Customer資料庫表格中搜尋使用者名稱。

      如果找不到用戶的名稱，請完成以下任務：

      * 如果 `Customer.IsSubscriber` 屬性設為 `true`，您需要為使用模型產生授 *`Subscription`* 權並傳送給使用者。

      * 在資料庫表中搜 `CustomerAuthorization` 索用戶名和內容ID的記錄。
      如果您可以找到使用者記錄，請完成下列工作：

      * 如果屬 `CustomerAuthorization.UsageType` 性設為， `DTO`請為DTO使用模式產生授權，並傳送給使用者。

      * 如果屬 `CustomerAuthorization.UsageType` 性設為，請 `VOD`為VOD使用模式產生授權，並傳送給使用者。
      如果DRM策略不允許匿名訪問，請完成以下任務：

      * 如果請求中沒有有效的驗證Token，您必須傳回「需要驗證」錯誤。
      * 否則傳回「未授權」錯誤。



* 如果其中一個DRM政策允許匿名存取，請為廣告資助的使用模式產生授權並傳送給使用者。

