---
description: com.adobe.mediacore.timeline.TimelineMarker介面現在包含一種新方法
title: 從2.5.x懶惰廣告解析升級到3.0.0懶惰廣告解析（API/工作流更改）
exl-id: 403ccb25-99a9-4545-9d17-3b71583bc6d8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 從2.5.x懶惰廣告解析升級到3.x懶惰廣告解析（API/工作流更改）:{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

com.adobe.mediacore.timeline.TimelineMarker介面現在包含一種新方法：

**Placement.Type getPlacementType()**

此方法將返回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL的放置類型。 如果廣告中斷未解決， `getDuration()`TimelineMarker介面上的方法將返回0。

>[!NOTE]
>
>如果尚未解析此介面，則它不會始終轉換為com.mediacore.timeline.advertising.AdBreakTimelineItem類型。 如果 `getDuration()` TimelineMarker的方法大於0。

**事件更改：**

`kEventAdResolutionComplete` 現在已折舊，現在在玩家進入PREPARED狀態後立即觸發。 以前只聽取此事件以繪製清理欄的應用程式應更改此項以偵聽 `kEventTimelineUpdated` 只是。 在解決單個廣告中斷後， `kEventTimelineUpdated` 將發送事件。
