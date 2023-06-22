---
description: 您可以指定是否在載入所有廣告並將其放置在時間軸中之前允許播放。 以此方式開始播放可讓檢視者更快速地存取主要內容。 此功能僅適用於即時DVR，不適用於例如VOD資產。
title: 啟用延遲廣告載入
exl-id: 6b70a7ae-28ce-4a19-9560-26e937c721cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 啟用延遲廣告載入{#enable-lazy-ad-loading}

您可以指定是否在載入所有廣告並將其放置在時間軸中之前允許播放。 以此方式開始播放可讓檢視者更快速地存取主要內容。 此功能僅適用於即時DVR，不適用於例如VOD資產。

1. 使用布林值屬性 `delayAdLoading` 在 `AdvertisingMetadata`.

   * 為false時，TVSDK會等到所有廣告都解析並置入後，才轉換為PREPARED狀態。 預設為false。
   * 為true時，TVSDK只會解析初始廣告和轉換到「已準備」狀態。 剩餘的廣告會在播放期間解析和置入。

1. 若要使用Adobe Primetime ad decisioning啟用延遲的廣告載入，請將此項設為 `true` 當您建立 `AuditudeSettings`.

   此 `AuditudeSettings` 類別繼承此屬性的來源 `AdvertisingMetadata`，但不繼承目前的值。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. 若要將廣告準確地反映為拖曳列上的提示，請聆聽 `TimelineEvent`. `TIMELINE_UPDATED` 事件，並在每次收到此事件時重繪清除列。

   當VoD資料流使用延遲的廣告載入時，當您的播放器進入「已準備」狀態時，並非所有廣告都會放在時間軸上，因此您必須明確重繪拖曳列。

   TVSDK會最佳化此事件的傳送，以將必須重繪拖曳列的次數減到最少；因此，時間軸事件的數量與要放置在時間軸上的廣告插播數量無關。 例如，如果您有5個廣告插播，您可能不會剛好收到5個事件。

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```
