---
description: 可以使用現有的懶惰廣告載入機制啟用或禁用懶惰廣告解析功能（預設情況下禁用懶惰廣告解析）。
keywords: Lazy;Ad resolving;Ad loading;delayLoading
title: 啟用延遲和解析
exl-id: a52a1f9a-3bf6-4193-8347-1ef248ba8884
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 啟用延遲和解析 {#enable-lazy-ad-resolving}

可以使用現有的懶惰廣告載入機制啟用或禁用懶惰廣告解析功能（預設情況下禁用懶惰廣告解析）。

您可以通過調用啟用或禁用懶惰廣告解決 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) 是真是假。

* 使用布爾值 *有延遲載入* 和 *setDelayAdLoading* AdvertingMetadata中的方法，用於控制廣告解析的時間安排和在時間線上放置廣告：

   * 如果 *有延遲載入* 返回false,TVSDK等待直到解析並放置所有廣告後才轉換為PREPARED狀態。
   * 如果 *有延遲載入* 返回true,TVSDK僅解析初始廣告並轉換到PREPARED狀態。

      * 其餘廣告在回放期間被解析和放置。
   * 當*hasPreroll *或 *有LivePreroll* 返回false時，TVSDK假定沒有預播廣告，並立即開始播放內容。 這些預設設定為true。


**與懶惰廣告解析相關的API:**

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

為了將廣告準確地反映為手術棒上的提示，請聆聽 `TimelineEvent`並在每次收到此事件時重新繪製清理欄。

當為VOD流啟用「懶惰廣告解析」時，所有廣告中斷都會放在時間線上，但是，許多廣告中斷仍無法解決。 應用程式可通過檢查 `TimelineMarker::getDuration()`。 如果值大於零，則廣告分段內的廣告已被解析。

TVSDK在解決廣告中斷時以及當播放器轉換到PREPARED狀態時調度此事件。

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
