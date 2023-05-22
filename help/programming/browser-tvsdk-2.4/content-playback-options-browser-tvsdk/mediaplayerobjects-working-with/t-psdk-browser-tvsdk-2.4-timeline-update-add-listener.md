---
description: 要接收有關時間線更新的通知，請註冊相應的事件偵聽器。
title: 為TimelineUpdatedEvent添加偵聽器
exl-id: 7b55beb5-fd84-4144-8d02-bbd998f99e3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# 為TimelineUpdatedEvent添加偵聽器{#add-listeners-for-timelineupdatedevent}

要接收有關時間線更新的通知，請註冊相應的事件偵聽器。

每次時間線更新時， `MediaPlayer` 派單 `AdobePSDK.TimelineEvent` 類型 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`。
1. 實施適當的偵聽器。

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
