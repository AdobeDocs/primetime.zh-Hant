---
description: com.adobe.mediacore.timeline.TimelineMarker介面現在包含新方法
title: 從2.5.x延遲廣告解決升級到3.0.0延遲廣告解決（API/工作流程變更）
exl-id: 403ccb25-99a9-4545-9d17-3b71583bc6d8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 從2.5.x延遲廣告解決升級為3.x延遲廣告解決（API/工作流程變更）：{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

com.adobe.mediacore.timeline.TimelineMarker介面現在包含新方法：

**Placement.Type getPlacementType()**

此方法會傳回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL等版位型別。 如果廣告插播未解析， `getDuration()`TimelineMarker介面上的方法將傳回0。

>[!NOTE]
>
>如果此介面尚未解析，則不會一律轉型為型別com.mediacore.timeline.advertising.AdBreakTimelineItem。 如果符合以下條件，則能夠強制轉換 `getDuration()` TimelineMarker的方法大於0。

**事件變更：**

`kEventAdResolutionComplete` 現已折舊，且播放器進入「已準備」狀態後會立即觸發。 先前僅監聽此事件以繪製拖曳列的應用程式應將此變更為監聽 `kEventTimelineUpdated` 僅限。 解決個別廣告插播後，新的 `kEventTimelineUpdated` 將會傳送事件。
