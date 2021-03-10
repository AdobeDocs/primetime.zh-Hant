---
description: 對於隨選視訊(VOD)內容，TVSDK會在主要內容中剪接廣告，以增加時間軸持續時間。
title: VOD廣告解析與插入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# VOD廣告解析和插入{#vod-ad-resolving-and-insertion}

對於隨選視訊(VOD)內容，TVSDK會在主要內容中剪接廣告，以增加時間軸持續時間。

在播放之前，TVSDK會解析已知廣告、在主要內容中插入廣告插播(如從Adobe Primetime廣告決策傳回的時間軸所述)，並視需要重新計算虛擬時間軸。

TVSDK會以下列方式插入廣告：

* **Pre-roll**，即內容之前。
* **Mid-roll**，即內容中。
* **Post-roll**，即在內容之後。

播放開始後，內容中不會再發生其他變更。 廣告不能是：

* 已插入
* 已刪除

   例如，您無法從內容中刪除內建廣告，以提供免廣告體驗。
* 已取代

   例如，您無法將內建廣告取代為目標廣告。

