---
description: SEES參考伺服器會示範如何使用ExpressPlay啟用裝置系結權益服務。
seo-description: SEES參考伺服器會示範如何使用ExpressPlay啟用裝置系結權益服務。
seo-title: 參考服務裝置系結權益
title: 參考服務裝置系結權益
uuid: 22ce2f8e-1758-4528-8caf-60d209839afe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 參考服務：裝置系結權益 {#reference-service-device-binding-entitlement}

SEES參考伺服器會示範如何使用ExpressPlay啟用裝置系結權益服務。

>[!NOTE]
>
>裝置綁定的權益服務也可以是時間限制，或提供租用期間。

若要引導 `device_id` 資訊，請播放虛擬M3U8內容。 然後，您可以將Cookie內嵌在ExpressPlay Token中、產生SPC(其中包 `device_id`含)，並傳送 `getToken` 至ExpressPlay伺服器。

![](assets/fees-device-binding.png)

序列從播放虛擬M3U8開始。 Cookie會傳送至SEES伺服器，以取得ExpressPlay Token URL。 在收到Cookie系結的ExpressPlay Token URL後，下一步是產生SPC並傳送至ExpressPlay伺服器。 ExpressPlay伺服器會從 `device_id` SPC（ExpressPlay Token URL中的Cookie）擷取，並將Cookie和 `device_id` 放入交易記錄。

用戶端會向SEES傳送相同的Cookie，提出實際的授權要求。 SEES會使用Cookie從ExpressPlay伺 `device_id` 服器擷取。

SEES會要求裝置系結的ExpressPlay Token以及時間系結的ExpressPlay Token，並將該Token傳回給用戶端。

用戶端使用ExpressPlay Token提出授權要求。

ExpressPlay伺服器將SPC `device_id` 中的與ExpressPlay令牌 `device_id` 中的進行比較。 ExpressPlay伺服器僅在兩個值匹配時才發 `device_id` 出許可證。
