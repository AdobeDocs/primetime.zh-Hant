---
description: 若要接收有關時間軸更新的通知，請註冊適當的事件接聽程式。
title: 新增時間軸UpdatedEvent的監聽器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# 為TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}添加監聽器

若要接收有關時間軸更新的通知，請註冊適當的事件接聽程式。

每次時間軸更新時，`MediaPlayer`都會以類型`AdobePSDK.PSDKEventType.TIMELINE_UPDATED`調度`AdobePSDK.TimelineEvent`。
1. 實作適當的監聽器。

   ```js
   function onTimelineUpdatedEvent(event) { 
       var timelineMarkers = event.timeline.timelineMarkers; 
       //add code to remove old timeline markers from scrub-bar. 
       var range = player.playbackRange; 
       //iterate through the list of timelineMarkers 
       for(var i = 0; i < timelineMarkers.length; i++) 
       { 
           var markerLocalTime = timelineMarkers[i].localRange.begin; 
           var markerVirtualTime = timelineMarkers[i].virtualRange.begin; 
           var duration = timelineMarkers[i].duration; 
        // add code to draw a particular marker on scrub-bar 
       }      
   }
   ```

1. 註冊事件偵聽器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```

