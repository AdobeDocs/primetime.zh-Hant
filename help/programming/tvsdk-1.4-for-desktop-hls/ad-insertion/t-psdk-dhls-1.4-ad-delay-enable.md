---
description: 可以指定是否在載入所有廣告並將其置於時間軸之前允許播放。 以這種方式開始播放，讓觀看者能夠更快地訪問主內容。 此功能僅適用於即時DVR，不適用，例如VOD資產。
title: 啟用懶散載入
exl-id: 6b70a7ae-28ce-4a19-9560-26e937c721cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 啟用懶散載入{#enable-lazy-ad-loading}

可以指定是否在載入所有廣告並將其置於時間軸之前允許播放。 以這種方式開始播放，讓觀看者能夠更快地訪問主內容。 此功能僅適用於即時DVR，不適用，例如VOD資產。

1. 使用布爾屬性 `delayAdLoading` 在 `AdvertisingMetadata`。

   * 如果為false，則TVSDK將等待，直到解析並放置所有廣告後，再轉換為PREPARED狀態。 預設為false。
   * 如果為true，則TVSDK僅解析初始廣告並轉換為PREPARED狀態。 其餘廣告在回放期間被解析和放置。

1. 要激活延遲廣告載入和Adobe Primetime廣告決策，請將此設定為 `true` 建立時 `AuditudeSettings`。

   的 `AuditudeSettings` 類繼承了此屬性 `AdvertisingMetadata`，但不繼承當前值。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. 為了將廣告準確地反映為手術棒上的提示，請聆聽 `TimelineEvent`。 `TIMELINE_UPDATED` 事件，並在每次收到此事件時重新繪製清理欄。

   當VoD流使用延遲的廣告載入時，當播放器進入PREPARED狀態時，並非所有廣告都放在時間軸上，因此您必須顯式重新繪製清理欄。

   TVSDK優化了此事件的派單，以最小化您必須重新繪製清理欄的次數；因此，時間線事件的數量與要放置在時間線上的廣告中斷的數量無關。 例如，如果您有五個廣告中斷，則可能不會收到五個事件。

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```
