---
description: 您可以指定在載入所有廣告並將其放置在時間軸中之前是否允許播放。 以此方式開始播放可讓檢視者更快速地存取主要內容。 此功能僅適用於即時DVR，不適用於如VOD資產。
title: 啟用延遲廣告載入
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 啟用延遲廣告載入{#enable-lazy-ad-loading}

您可以指定在載入所有廣告並將其放置在時間軸中之前是否允許播放。 以此方式開始播放可讓檢視者更快速地存取主要內容。 此功能僅適用於即時DVR，不適用於如VOD資產。

1. 使用布林值屬性 `delayAdLoading` 在 `AdvertisingMetadata`.

   * 為false時，TVSDK會等到所有廣告解決並放置後，再轉換為PREPARED狀態。 預設為false。
   * 為true時，TVSDK僅解析初始廣告和轉換為「已準備」狀態。 剩餘的廣告會在播放期間解析並置入。

1. 若要使用Adobe Primetime ad decisioning啟用延遲的廣告載入，請將此項設為 `true` 當您建立 `AuditudeSettings`.

   此 `AuditudeSettings` 類別會從繼承此屬性 `AdvertisingMetadata`，但不繼承目前值。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. 若要準確將廣告反映為拖曳列上的提示，請聆聽 `TimelineEvent`. `TIMELINE_UPDATED` 事件，並在每次收到此事件時重新繪製拖曳列。

   當VoD資料流使用延遲的廣告載入時，當您的播放器進入「已準備」狀態時，並非所有廣告都會放在時間軸上，因此您必須明確重新繪製拖曳列。

   TVSDK會最佳化此事件的傳送，以將必須重新繪製拖曳列的次數減至最少；因此，時間軸事件的數量與要放置在時間軸上的廣告插播數量無關。 例如，如果您有五個廣告插播，您可能不會收到剛好五個事件。

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```
