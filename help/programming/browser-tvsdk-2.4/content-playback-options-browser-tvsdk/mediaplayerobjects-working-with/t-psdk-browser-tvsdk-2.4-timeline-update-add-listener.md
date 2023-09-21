---
description: 若要接收關於時間表更新的通知，請註冊適當的事件接聽程式。
title: 新增TimelineUpdatedEvent的監聽器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# 新增TimelineUpdatedEvent的監聽器{#add-listeners-for-timelineupdatedevent}

若要接收關於時間表更新的通知，請註冊適當的事件接聽程式。

每次更新時間軸時， `MediaPlayer` 派單 `AdobePSDK.TimelineEvent` 與型別 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. 實作適當的接聽程式。

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

1. 註冊事件接聽程式。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```
