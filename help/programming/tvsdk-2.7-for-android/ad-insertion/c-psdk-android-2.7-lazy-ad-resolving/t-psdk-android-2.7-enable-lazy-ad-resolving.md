---
description: 可以使用現有的懶惰廣告載入機制啟用或禁用懶惰廣告解析功能（預設情況下啟用了懶惰廣告解析）。
keywords: Lazy;Ad resolving;Ad loading;delayLoading
title: 啟用延遲和解析
exl-id: 4cd53ace-b0f5-4eef-93c3-644c2f48ce49
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 啟用延遲和解析 {#enable-lazy-ad-resolving}

可以使用現有的懶惰廣告載入機制啟用或禁用懶惰廣告解析功能（預設情況下啟用了懶惰廣告解析）。

您可以通過調用啟用或禁用懶惰廣告解決 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) 與 `true` 或 `false`。

1. 使用布爾值 `hasDelayAdLoading` 和 `setDelayAdLoading` 方法 `AdvertisingMetadata` 控制廣告解析的時間安排和時間線上廣告的放置：

   * 如果 `hasDelayAdLoading` 返回false,TVSDK等待直到解析並放置所有廣告後才轉換為PREPARED狀態。
   * 如果 `hasDelayAdLoading` 返回true,TVSDK僅解析初始廣告並轉換到PREPARED狀態。 其餘廣告在回放期間被解析和放置。
   * 當 `hasPreroll` 或 `hasLivePreroll` 返回false時，TVSDK假定沒有預播廣告，並立即開始播放內容。 這些預設值為true。

      與懶惰廣告解析相關的API:

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

1. 為了將廣告準確地反映為手術棒上的提示，請聆聽 `TimelineEvent` 事件，並在每次收到此事件時重新繪製清理欄。

   當為VOD流啟用「懶惰廣告解析」時，並非所有廣告都會在播放器進入PREPARED狀態時置於時間線上，因此您的播放器必須顯式地重新繪製清理欄。

   TVSDK優化了此事件的派單，以最小化您必須重新繪製清理欄的次數；因此，時間線事件的數量與要放置在時間線上的廣告中斷的數量無關。 例如，如果您有五個廣告中斷，則可能不會收到五個事件。

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

>要驗證是否啟用或禁用「懶惰廣告解析」功能，請調用 `AdvertisingMetadata.hasDelayAdLoading`。 返回值 `true` 表示已啟用懶惰廣告解決； `false` 表示功能已禁用。
