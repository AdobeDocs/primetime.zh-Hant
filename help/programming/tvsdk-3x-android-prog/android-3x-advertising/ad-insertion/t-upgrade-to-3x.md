---
description: com.adobe.mediacore.timeline.TimelineMarker介面現在包含新方法
title: 從2.5.x延遲廣告解決升級到3.0.0延遲廣告解決（API/工作流程變更）
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 從2.5.x延遲廣告解決升級到3.x延遲廣告解決（API/工作流程變更）：{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

com.adobe.mediacore.timeline.TimelineMarker介面現在包含新方法：

**Placement.Type getPlacementType()**

此方法會傳回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL等版位型別。 如果廣告插播未解決， `getDuration()`TimelineMarker介面上的方法將傳回0。

>[!NOTE]
>
>如果尚未解析此介面，則它不會始終轉換為型別com.mediacore.timeline.advertising.AdBreakTimelineItem。 如果符合以下條件，則能夠強制轉換： `getDuration()` TimelineMarker的方法大於0。

**事件變更：**

`kEventAdResolutionComplete` 現在已折舊，而且會在播放器進入「已準備」狀態後立即觸發。 先前僅監聽此事件以繪製拖曳列的應用程式應將此變更成監聽 `kEventTimelineUpdated` 僅限。 解決個別廣告插播後，新的 `kEventTimelineUpdated` 將會傳送事件。
