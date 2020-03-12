---
description: 您可以使用現有的「延遲廣告載入」機制來啟用或停用「延遲廣告解析」功能（預設會停用「延遲廣告解析」）。
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: 您可以使用現有的「延遲廣告載入」機制來啟用或停用「延遲廣告解析」功能（預設會停用「延遲廣告解析」）。
seo-title: 啟用延遲廣告解析
title: 啟用延遲廣告解析
uuid: 91884eea-a622-4f5d-b6a8-36bb0050ba1d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 啟用延遲廣告解析 {#enable-lazy-ad-resolving}

您可以使用現有的「延遲廣告載入」機制來啟用或停用「延遲廣告解析」功能（預設會停用「延遲廣告解析」）。

您可以呼叫 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) with true or false，以啟用或停用「懶惰廣告解析」。

* 使用AdvertisingMetadata中 *的Boolean hasDelayAdLoading* and *setDelayAdLoading* 方法，控制廣告解析的時間，以及時間軸上廣告的位置：

   * 如果 *hasDelayAdLoading傳回false* ,TVSDK會等到所有廣告都解析並放置，再轉換至PREPARED狀態。
   * 如果 *hasDelayAdLoading傳回true* ,TVSDK只會解析初始廣告並轉換至PREPARED狀態。

      * 其餘廣告會在播放期間解析並放置。
   * 當*hasPreroll *或 *hasLivePreroll* return false時，TVSDK會假設沒有前置廣告，並立即開始播放內容。 這些預設為true。


**與延遲廣告解析度相關的API:**

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

若要將廣告準確反映為拖曳列上的提示，請監聽 `TimelineEvent`事件，並在每次收到此事件時重新繪製拖曳列。

當VOD串流啟用「延遲廣告解析」時，所有廣告插播都會放在時間軸上，但許多廣告插播仍無法解決。 應用程式可以透過檢查來判斷是否繪製這些標籤 `TimelineMarker::getDuration()`。 如果值大於零，則廣告分段內的廣告已解決。

TVSDK會在廣告中斷已解決時，以及當播放器轉換為「已準備」狀態時，派單此事件。

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
