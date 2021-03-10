---
description: 對於隨選視訊(VOD)內容，TVSDK會在主要內容中剪接廣告，以增加時間軸持續時間。
title: 解析並插入VOD廣告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 解析並插入VOD廣告{#resolve-and-insert-vod-ad}

對於隨選視訊(VOD)內容，TVSDK會在主要內容中剪接廣告，以增加時間軸持續時間。

在播放之前，TVSDK會解析已知廣告、在主要內容中插入廣告插播(如從Adobe Primetime廣告決策傳回的時間軸所述)，並視需要重新計算虛擬時間軸。

TVSDK會以下列方式插入廣告：

* **前置卷**，會置於內容之前。
* **Mid-roll**，位於內容中間。
* **後置卷**，會置於內容後面。

>[!TIP]
>
>播放開始後，內容中不會再發生其他變更。

廣告不能是：

* 已插入
* 已刪除

   例如，您無法從內容中刪除內建廣告，以提供免廣告體驗。
* 已取代

   例如，您無法將內建廣告取代為目標廣告。

