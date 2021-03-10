---
description: 對於隨選視訊(VOD)內容，TVSDK會在主要內容中剪接廣告，以增加時間軸持續時間。
title: VOD廣告解析與插入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# VOD廣告解析和插入{#vod-ad-resolving-and-insertion}

對於隨選視訊(VOD)內容，TVSDK會在主要內容中剪接廣告，以增加時間軸持續時間。

播放前，TVSDK會解析已知廣告、在主要內容中插入廣告分段（如從TVSDK傳回的時間軸所述），並視需要重新計算虛擬時間軸。

TVSDK會以下列方式插入廣告：

* **Pre-roll**，即內容之前。
* **Mid-roll**，即內容中。
* **Post-roll**，即在內容之後。

>[!IMPORTANT]
>
>實作自訂`AdPolicySelector`時，可根據`AdBreakTimelineItem`的類型，為`AdPolicyInfo`中的每種`AdBreakTimelineItem`類型（前滾、中滾或後滾）指定不同的原則。 例如，您可以在播放中段內容後保留該內容，但在播放後移除前段內容。

播放開始後，內容中不會再發生其他變更。 廣告不能是：

* 已插入
* 已刪除

   例如，您無法從內容中刪除內建廣告，以提供免廣告體驗。
* 已取代

   例如，您無法將內建廣告取代為目標廣告。

