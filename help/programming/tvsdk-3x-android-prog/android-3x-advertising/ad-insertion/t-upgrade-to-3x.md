---
description: 'com.adobe.mediacore.timeline.TimelineMarker介面現在包含新方法 '
title: '從2.5.x懶惰廣告解析升級至3.0.0懶惰廣告解析（API/工作流程變更） '
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# 從2.5.x懶惰廣告解析升級至3.x懶惰廣告解析（API/工作流程變更）:{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

com.adobe.mediacore.timeline.TimelineMarker介面現在包含新方法：

**Placement.Type getPlacementType()**

此方法將返回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL的放置類型。 如果廣告中斷未解析，TimelineMarker介面上的`getDuration()`方法將會傳回0。

>[!NOTE]
>
>如果尚未解決此介面，它不一定會轉存至com.mediacore.timeline.advertising.AdBreakTimelineItem類型。 如果時間軸標籤的`getDuration()`方法大於0，則可以進行分機。

**事件變更：**

`kEventAdResolutionComplete` 現在會折舊，並在玩家進入PREPARED狀態後立即觸發。先前只聽取此事件以繪製拖曳列的應用程式，應將此變更為僅監聽`kEventTimelineUpdated`。 解決個別廣告插播後，將會傳送新的`kEventTimelineUpdated`事件。
