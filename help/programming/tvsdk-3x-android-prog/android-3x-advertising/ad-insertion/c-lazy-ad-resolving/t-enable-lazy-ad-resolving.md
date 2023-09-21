---
description: 您可以使用現有的延遲廣告載入機制來啟用或停用延遲廣告解析功能（預設會停用延遲廣告解析）。
keywords: 延遲；廣告解析；廣告載入；delayLoading
title: 啟用延遲廣告解析
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 啟用延遲廣告解析 {#enable-lazy-ad-resolving}

您可以使用現有的延遲廣告載入機制來啟用或停用延遲廣告解析功能（預設會停用延遲廣告解析）。

您可以透過呼叫來啟用或停用延遲廣告解析 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) 為true或false。

* 使用布林值 *hasDelayAdloading* 和 *setDelayAdloading* 控制AdvertisingMetadata中廣告解析時間及廣告在時間軸上置入位置的方法：

   * 如果 *hasDelayAdloading* 傳回false，TVSDK會等到所有廣告解決並放置後，才轉換為PREPARED狀態。
   * 如果 *hasDelayAdloading* 傳回true，TVSDK只會解析初始廣告和轉換到「已準備」狀態。

      * 剩餘的廣告會在播放期間解析並置入。

   * 當*hasPreroll *或 *hasLivePreroll* return false，TVSDK會假設沒有前段廣告，並立即開始播放內容。 這些預設值設為true。

**與延遲廣告解析度相關的API：**

```
Class:    com.adobe.mediacore.metadata.AdvertisingMetadata 
Methods: 
    public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
    public final void setDelayAdLoading() // Enable or disable Lazy Ad Resolving 
    public final void setDelayAdLoadingTolerance() // Sets the Lazy Ad Resolving Tolerance level.  This value is added to the BufferControlParameters::playBufferTime and the content's EXT-X-TARGETDURATION to determine when ad breaks should resolve 
    public final double getDelayAdLoadingTolerance() // Gets the Lazy Ad Resolving Tolerance level 
    public final boolean hasPreroll() // Check for existence of pre-roll ads 
    public final void setPreroll() // Set pre-roll true or false 
    public final boolean hasLivePreroll() // Check for live pre-roll ads 
    public final void setLivePreroll() // Set live pre-roll true or false

Class:     com.adobe.mediacore.timeline.TimelineMarker 
Methods: 
    public double getDuration() // Returns the current duration of the TimelineMarker.  This will be zero if the ad break has not yet resolved. 
    public Placement.Type getPlacementType() // Returns whether
```

若要準確將廣告反映為拖曳列上的提示，請聆聽 `TimelineEvent`事件，並在每次收到此事件時重新繪製拖曳列。

為VOD資料流啟用延遲廣告解決時，所有廣告插播都會放置在時間軸上，但是，許多廣告插播尚未解決。 應用程式可藉由檢查 `TimelineMarker::getDuration()`. 如果值大於零，則表示廣告插播中的廣告已解決。

TVSDK會在廣告插播解決後，以及播放器轉換為「已準備」狀態時傳送此事件。

```
mediaPlayer.addEventListener(MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
/** 
* ... 
*/ 
public void onTimelineUpdated(TimelineEvent event) { 
for (PlaybackManagerEventListener listener : eventListeners) { 
  listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
}
```
