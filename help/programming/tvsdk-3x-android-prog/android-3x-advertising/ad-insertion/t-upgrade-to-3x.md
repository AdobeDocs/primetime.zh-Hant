---
description: 'com.adobe.mediacore.timeline.TimelineMarker介面現在包含新方法 '
seo-description: 'com.adobe.mediacore.timeline.TimelineMarker介面現在包含新方法 '
seo-title: '從2.5.x懶惰廣告解析升級至3.0.0懶惰廣告解析（API/工作流程變更） '
title: '從2.5.x懶惰廣告解析升級至3.0.0懶惰廣告解析（API/工作流程變更） '
uuid: 5870ceb4-93a8-4c8b-b716-673396122644
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 從2.5.x延遲廣告解析升級至3.x延遲廣告解析（API/工作流程變更）:{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

com.adobe.mediacore.timeline.TimelineMarker介面現在包含新方法：

**Placement.Type getPlacementType()**

此方法將返回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL的放置類型。 如果廣告中斷未解析，TimelineMarker `getDuration()`介面上的方法將返回0。

>[!NOTE]
>
>如果尚未解決此介面，它不一定會轉存至com.mediacore.timeline.advertising.AdBreakTimelineItem類型。 如果時間軸標籤的方 `getDuration()` 法大於0，則可進行分機。

**事件變更：**

`kEventAdResolutionComplete` 現在會折舊，並在玩家進入PREPARED狀態後立即觸發。 先前只聽取此活動以繪製拖曳列的應用程式，應將此變更為僅監聽 `kEventTimelineUpdated` 項目。 解決個別廣告插播後，會傳 `kEventTimelineUpdated` 送新事件。
