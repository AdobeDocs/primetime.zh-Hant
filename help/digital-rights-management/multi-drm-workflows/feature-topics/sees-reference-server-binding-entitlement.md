---
description: SEES參考伺服器會示範如何使用ExpressPlay啟用裝置繫結軟體權利檔案服務。
title: 參考服務裝置繫結權益
exl-id: 91f9d406-f3f9-47d3-aa50-f47c4e81b9fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 參考服務：裝置繫結權益 {#reference-service-device-binding-entitlement}

SEES參考伺服器會示範如何使用ExpressPlay啟用裝置繫結軟體權利檔案服務。

>[!NOTE]
>
>裝置繫結權益服務也可以是時間繫結或提供租用期間。

若要啟動 `device_id` 資訊，播放虛擬M3U8內容。 然後，您可以在ExpressPlay權杖中內嵌Cookie，產生SPC (其中包含 `device_id`)，並傳送 `getToken` 至ExpressPlay伺服器。

![](assets/fees-device-binding.png)

此序列會先播放一個虛擬M3U8。 Cookie會傳送至SEES伺服器，以取得ExpressPlay權杖URL。 在收到Cookie繫結的ExpressPlay權杖URL後，下一步是產生SPC並將其傳送到ExpressPlay伺服器。 ExpressPlay伺服器會提取 `device_id` 從SPC、ExpressPlay權杖URL的Cookie，並將Cookie和 `device_id` 在交易記錄中。

使用者端會向傳送相同Cookie的SEES提出真正的授權請求。 SEES會採用Cookie來擷取 `device_id` 從ExpressPlay伺服器。

SEES會要求裝置界限和時間界限的ExpressPlay權杖，並將該Token傳回使用者端。

使用者端使用ExpressPlay權杖提出授權請求。

ExpressPlay伺服器會比較 `device_id` 在SPC中，使用 `device_id` 在ExpressPlay權杖中。 ExpressPlay伺服器只會在兩者 `device_id` 值相符。
