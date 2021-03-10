---
description: 您可以指定是否允許在所有廣告載入並置於時間軸之前播放。 以這種方式開始播放，讓檢視者可更快速存取主要內容。 此功能僅適用於即時DVR，而且無法使用，例如VOD資產。
title: 啟用延遲廣告載入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# 啟用延遲廣告載入{#enable-lazy-ad-loading}

您可以指定是否允許在所有廣告載入並置於時間軸之前播放。 以這種方式開始播放，讓檢視者可更快速存取主要內容。 此功能僅適用於即時DVR，而且無法使用，例如VOD資產。

1. 使用`AdvertisingMetadata`中的Boolean屬性`delayAdLoading`。

   * 若為false,TVSDK會等到所有廣告都解決並放置後，再轉換至PREPARED狀態。 預設為false。
   * 若為true,TVSDK只會解析初始廣告和轉場至「已準備」狀態。 其餘廣告會在播放期間解析並放置。

1. 若要啟用延遲的廣告載入，請在您建立`AuditudeSettings`時，將此設定為`true`。

   `AuditudeSettings`類繼承了`AdvertisingMetadata`的此屬性，但不繼承當前值。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. 若要將廣告準確反映為拖曳列上的提示，請監聽`TimelineEvent`。 `TIMELINE_UPDATED` 活動，並在您每次收到此活動時重新繪製拖曳列。

   當VoD串流使用延遲廣告載入時，並非播放器進入「已準備」狀態時，所有廣告都會放在時間軸上，因此您必須明確重繪拖曳列。

   TVSDK會最佳化此事件的派單，將您必須重繪拖曳列的次數減至最少；因此，時間軸事件的數目與要放置在時間軸上的廣告分段數目無關。 例如，如果您有五個廣告插播，可能就不會收到五個事件。

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

