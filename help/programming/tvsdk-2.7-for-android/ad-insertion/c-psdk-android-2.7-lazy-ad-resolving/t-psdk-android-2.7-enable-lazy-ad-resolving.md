---
description: 您可以使用現有的延遲廣告載入機制來啟用或停用延遲廣告解析功能（預設為啟用延遲廣告解析）。
keywords: 延遲；廣告解析；廣告載入；delayLoading
title: 啟用延遲廣告解析
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 啟用延遲廣告解析 {#enable-lazy-ad-resolving}

您可以使用現有的延遲廣告載入機制來啟用或停用延遲廣告解析功能（預設為啟用延遲廣告解析）。

您可以透過呼叫來啟用或停用延遲廣告解析 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) 替換為 `true` 或 `false`.

1. 使用布林值 `hasDelayAdLoading` 和 `setDelayAdLoading` 中的方法 `AdvertisingMetadata` 若要控制廣告解析的時間以及在時間軸上的廣告位置：

   * 如果 `hasDelayAdLoading` 傳回false，TVSDK會等到所有廣告解決並放置後，才轉換為PREPARED狀態。
   * 如果 `hasDelayAdLoading` 傳回true，TVSDK只會解析初始廣告和轉換到「已準備」狀態。 剩餘的廣告會在播放期間解析並置入。
   * 時間 `hasPreroll` 或 `hasLivePreroll` return false，TVSDK會假設沒有前段廣告，並立即開始播放內容。 這些預設為true。

     與延遲廣告解析度相關的API：

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

1. 若要準確將廣告反映為拖曳列上的提示，請聆聽 `TimelineEvent` 事件，並在每次收到此事件時重新繪製拖曳列。

   為VOD資料流啟用延遲廣告解決時，當您的播放器進入「已準備」狀態時，並非所有廣告都會放置在時間軸上，因此您的播放器必須明確重新繪製拖曳列。

   TVSDK會最佳化此事件的傳送，以將必須重新繪製拖曳列的次數減至最少；因此，時間軸事件的數量與要放置在時間軸上的廣告插播數量無關。 例如，如果您有五個廣告插播，您可能不會收到剛好五個事件。

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

>若要確認延遲廣告解決功能已啟用或已停用，請呼叫 `AdvertisingMetadata.hasDelayAdLoading`. 傳回值為 `true` 表示已啟用緩慢廣告解析； `false` 表示此功能已停用。
