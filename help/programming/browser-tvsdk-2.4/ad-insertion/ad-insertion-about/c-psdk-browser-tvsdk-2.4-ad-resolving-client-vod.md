---
description: 對於隨選視訊(VOD)內容，瀏覽器TVSDK會在主要內容中剪接廣告，以增加時間軸持續時間。
seo-description: 對於隨選視訊(VOD)內容，瀏覽器TVSDK會在主要內容中剪接廣告，以增加時間軸持續時間。
seo-title: VOD廣告解析與插入
title: VOD廣告解析與插入
uuid: 34a30ae5-d553-4c5d-9829-8e5eaa41c104
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# VOD廣告解析和插入{#vod-ad-resolving-and-insertion}

對於隨選視訊(VOD)內容，瀏覽器TVSDK會在主要內容中剪接廣告，以增加時間軸持續時間。

在播放之前，瀏覽器TVSDK會解析已知廣告、在主要內容中插入廣告插入（如Adobe Primetime廣告決策傳回的時間軸所述），並視需要重新計算虛擬時間軸。

瀏覽器TVSDK會以下列方式插入廣告：

* **Pre-roll**，即內容之前。
* **Post-roll**，即在內容之後。

播放開始後，內容中不會再發生其他變更。 廣告不能是：

* 已插入
* 已刪除

   例如，您無法從內容中刪除內建廣告，以提供免廣告體驗。
* 已取代

   例如，您無法將內建廣告取代為目標廣告。

