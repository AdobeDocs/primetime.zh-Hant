---
description: 針對隨選影片(VOD)內容，TVSDK會在主要內容中拼接廣告，插入廣告插播，以增加時間軸持續時間。
title: VOD廣告解析和插入
exl-id: 6f02c7fc-028d-442f-92d4-9efa671b7f02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# VOD廣告解析和插入{#vod-ad-resolving-and-insertion}

針對隨選影片(VOD)內容，TVSDK會在主要內容中拼接廣告，插入廣告插播，以增加時間軸持續時間。

在播放之前，TVSDK會解析已知廣告、依照TVSDK傳回之時間軸的說明，在主要內容中插入廣告插播，並在必要時重新計算虛擬時間軸。

TVSDK會以下列方式插入廣告：

* **前置滾動**，即內容之前。
* **中間滾動**，即位於內容中。
* **後置滾動**，在內容之後。

>[!IMPORTANT]
>
>實作自訂時 `AdPolicySelector`，則可以為每種型別指定不同的原則 `AdBreakTimelineItem` （前段、中段或後段） `AdPolicyInfo`，根據 `AdBreakTimelineItem`. 例如，您可以在播放後保留中段內容，但在播放後移除前段內容。

播放開始後，內容中不會發生其他變更。 廣告不可為：

* 已插入
* 已刪除

   例如，您無法從內容中刪除內建廣告以提供無廣告體驗。
* 已取代

   例如，您無法將內建廣告取代為目標廣告。
