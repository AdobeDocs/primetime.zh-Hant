---
description: 若要接收有關時間軸更新的通知，請註冊適當的事件接聽程式。
seo-description: 若要接收有關時間軸更新的通知，請註冊適當的事件接聽程式。
seo-title: 新增時間軸UpdatedEvent的監聽器
title: 新增時間軸UpdatedEvent的監聽器
uuid: 7d742e15-5a55-4155-93a7-7b79f21c1472
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 新增時間軸UpdatedEvent的監聽器{#add-listeners-for-timelineupdatedevent}

若要接收有關時間軸更新的通知，請註冊適當的事件接聽程式。

每次時間軸更新時，都會 `MediaPlayer` 使用 `AdobePSDK.TimelineEvent` 類型派單 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`。
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

