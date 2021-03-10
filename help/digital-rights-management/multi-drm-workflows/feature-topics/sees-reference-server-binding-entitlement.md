---
description: SEES參考伺服器會示範如何使用ExpressPlay啟用裝置系結權益服務。
title: 參考服務裝置系結權益
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# 參考服務：裝置系結權益{#reference-service-device-binding-entitlement}

SEES參考伺服器會示範如何使用ExpressPlay啟用裝置系結權益服務。

>[!NOTE]
>
>裝置綁定的權益服務也可以是時間限制，或提供租用期間。

若要引導`device_id`資訊，請播放虛擬M3U8內容。 然後，您可以將Cookie內嵌在ExpressPlay Token中，產生SPC（其中包含`device_id`），並傳送`getToken`至ExpressPlay伺服器。

![](assets/fees-device-binding.png)

序列從播放虛擬M3U8開始。 Cookie會傳送至SEES伺服器，以取得ExpressPlay Token URL。 在收到Cookie系結的ExpressPlay Token URL後，下一步是產生SPC並傳送至ExpressPlay伺服器。 ExpressPlay伺服器從SPC提取`device_id`，從ExpressPlay令牌URL提取Cookie，並將Cookie和`device_id`放入事務日誌中。

用戶端會向SEES傳送相同的Cookie，提出實際的授權要求。 SEES使用Cookie從ExpressPlay伺服器擷取`device_id`。

SEES會要求裝置系結的ExpressPlay Token以及時間系結的ExpressPlay Token，並將該Token傳回給用戶端。

用戶端使用ExpressPlay Token提出授權要求。

ExpressPlay伺服器將SPC中的`device_id`與ExpressPlay令牌中的`device_id`進行比較。 ExpressPlay伺服器僅在兩個`device_id`值匹配時發出許可證。
