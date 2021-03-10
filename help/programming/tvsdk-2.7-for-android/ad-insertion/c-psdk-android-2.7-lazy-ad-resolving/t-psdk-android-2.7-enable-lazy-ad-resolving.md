---
description: 您可以使用現有的「延遲廣告載入」機制來啟用或停用「延遲廣告解析」功能（預設會啟用「延遲廣告解析」）。
keywords: Lazy;Ad resoling;Ad loading;delayLoading
title: 啟用延遲廣告解析
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# 啟用延遲廣告解析{#enable-lazy-ad-resolving}

您可以使用現有的「延遲廣告載入」機制來啟用或停用「延遲廣告解析」功能（預設會啟用「延遲廣告解析」）。

您可以呼叫[AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-)（含`true`或`false`），以啟用或停用「懶惰廣告解決」。

1. 使用`AdvertisingMetadata`中的布林`hasDelayAdLoading`和`setDelayAdLoading`方法，控制廣告解析度的時間以及廣告在時間軸上的位置：

   * 如果`hasDelayAdLoading`傳回false,TVSDK會等到所有廣告都解析並放置，再轉換至PREPARED狀態。
   * 如果`hasDelayAdLoading`傳回true,TVSDK只會解析初始廣告和轉場至PREPARED狀態。 其餘廣告會在播放期間解析並放置。
   * 當`hasPreroll`或`hasLivePreroll`傳回false時，TVSDK會假設沒有前置廣告，並立即開始播放內容。 這些預設為true。

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

1. 若要將廣告準確反映為拖曳列上的提示，請監聽`TimelineEvent`事件，並在每次收到此事件時重新繪製拖曳列。

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

>若要確認「懶惰廣告解析」功能是啟用還是停用，請呼叫`AdvertisingMetadata.hasDelayAdLoading`。 傳回值`true`表示已啟用「懶惰廣告解析」;`false`表示功能已停用。

