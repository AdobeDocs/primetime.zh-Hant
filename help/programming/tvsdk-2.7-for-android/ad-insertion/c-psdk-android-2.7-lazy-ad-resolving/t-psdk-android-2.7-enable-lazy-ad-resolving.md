---
description: 您可以使用現有的「延遲廣告載入」機制來啟用或停用「延遲廣告解析」功能（預設會啟用「延遲廣告解析」）。
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: 您可以使用現有的「延遲廣告載入」機制來啟用或停用「延遲廣告解析」功能（預設會啟用「延遲廣告解析」）。
seo-title: 啟用延遲廣告解析
title: 啟用延遲廣告解析
uuid: a084ee0b-53af-4600-91f6-d30ccc89699d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 啟用延遲廣告解析 {#enable-lazy-ad-resolving}

您可以使用現有的「延遲廣告載入」機制來啟用或停用「延遲廣告解析」功能（預設會啟用「延遲廣告解析」）。

您可以使用或呼叫 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) ，以啟用或停 `true` 用懶散廣告解 `false`析。

1. 使用中的 `hasDelayAdLoading` 布林 `setDelayAdLoading` 和方 `AdvertisingMetadata` 法，控制廣告解析的時間以及廣告在時間軸上的位置：

   * 如果 `hasDelayAdLoading` 傳回false,TVSDK會等到所有廣告都解決並放置後，再轉換至PREPARED狀態。
   * 如果 `hasDelayAdLoading` 傳回true,TVSDK只會解析初始廣告和轉場至PREPARED狀態。 其餘廣告會在播放期間解析並放置。
   * 當 `hasPreroll` 或 `hasLivePreroll` 傳回false時，TVSDK會假設沒有前置廣告，並立即開始播放內容。 這些預設為true。

      與延遲廣告解析度相關的API:

      ```
      Class: 
         com.adobe.mediacore.metadata.AdvertisingMetadata 
      
      Methods: 
      […] 
          public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
          public final void setDelayAdLoading()    // Enable or disable Lazy Ad Resolving 
          public final boolean hasPreroll()        // Check for existence of pre-roll ads 
          public final void setPreroll()           // Set pre-roll true or false 
          public final boolean hasLivePreroll()    // Check for live pre-roll ads 
          public final void setLivePreroll()       // Set live pre-roll true or false 
      […]
      ```

1. 若要將廣告準確反映為拖曳列上的提示，請監聽該事 `TimelineEvent` 件，並在每次收到此事件時重新繪製拖曳列。

   當VOD串流啟用「延遲廣告解析」時，並非播放器進入「已準備」狀態時，所有廣告都會放在時間軸上，因此您的播放器必須明確重繪拖曳列。

   TVSDK會最佳化此事件的派單，將您必須重繪拖曳列的次數減至最少；因此，時間軸事件的數目與要放置在時間軸上的廣告分段數目無關。 例如，如果您有五個廣告插播，可能就不會收到五個事件。

   ```java
   mediaPlayer.addEventListener 
       (MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
   /** 
    * ... 
    */ 
   public void onTimelineUpdated(TimelineEvent event) { 
   
       for (PlaybackManagerEventListener listener : eventListeners) { 
           listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
       } 
   } 
   ```

>若要確認是否啟用或停用「懶惰廣告解析」功能，請呼叫 `AdvertisingMetadata.hasDelayAdLoading`。 傳回值表示啟 `true` 用「懶惰廣告解析」;表 `false` 示功能已停用。

