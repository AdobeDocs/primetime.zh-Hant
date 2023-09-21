---
description: 對於隨選影片(VOD)內容，TVSDK會將廣告分割插入主要內容，讓時間軸持續時間增加。
title: VOD廣告解析和插入
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# VOD廣告解析和插入{#vod-ad-resolving-and-insertion}

對於隨選影片(VOD)內容，TVSDK會將廣告分割插入主要內容，讓時間軸持續時間增加。

在播放之前，TVSDK會解析已知廣告、依照TVSDK傳回之時間軸的說明在主要內容中插入廣告插播，並在必要時重新計算虛擬時間軸。

TVSDK會以下列方式插入廣告：

* **前置滾動**，在內容之前。
* **中間滾動**，即位於內容中。
* **後置滾動**，在內容之後。

>[!IMPORTANT]
>
>實作自訂時 `AdPolicySelector`，您可以為每種型別提供不同的原則 `AdBreakTimelineItem` （前段、中段或後段） `AdPolicyInfo`，根據 `AdBreakTimelineItem`. 例如，您可以在播放中段內容後保留該內容，但在播放前段內容後將其移除。

播放開始後，內容不會發生其他變更。 廣告不得為：

* 已插入
* 已刪除

  例如，您無法從內容中刪除內建廣告以提供無廣告體驗。
* 已取代

  例如，您無法將內建廣告取代為目標廣告。
