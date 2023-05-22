---
description: 使用MediaPlayerItemLoader可幫助您獲取有關媒體流的資訊，而無需實例化MediaPlayer實例。 這在預緩衝流中特別有用，以便可以無延遲地開始回放。
title: 使用MediaPlayerItemLoader載入媒體資源
exl-id: 6bd081bb-b92b-4c0a-a3bc-ef2128d0d8bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader載入媒體資源 {#load-a-media-resource-using-mediaplayeritemloader}

使用MediaPlayerItemLoader可幫助您獲取有關媒體流的資訊，而無需實例化MediaPlayer實例。 這在預緩衝流中特別有用，以便可以無延遲地開始回放。

的 `MediaPlayerItemLoader` 類可幫助您為當前介質交換介質資源 `MediaPlayerItem` 不將視圖附加到 `MediaPlayer` 實例，它將分配視頻解碼硬體資源。 對於受DRM保護的內容，需要執行其他步驟，但本手冊沒有描述這些步驟。

>[!IMPORTANT]
>
>TVSDK不支援單個 `QoSProvider` 與兩者合作 `itemLoader` 和 `MediaPlayer`。 如果您的應用程式使用「即時開啟」，則應用程式需要維護兩個 `QoS` 實例並管理兩個實例以獲取資訊。 請參閱  [即開](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) 的子菜單。

1. 建立實例 `MediaPlayerItemLoader`。

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
   
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
   
           public void onBufferingBegin() { 
               //Do something 
           } 
   
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       }); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   } 
   ```

   >[!TIP]
   >
   >建立單獨的實例 `MediaPlayerItemLoader` 為每個資源。 不要使用 `MediaPlayerItemLoader` 實例以載入多個資源。

1. 實施 `ItemLoaderListener` 類，以接收來自 `MediaPlayerItemLoader` 實例。

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
           public void onBufferingBegin() { 
               //Do something 
           } 
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       } ); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   }
   ```

   在 `onLoadComplete()` 回調，執行下列操作之一：

   * 確保任何可能影響緩衝的內容（例如，選擇WebVTT或音頻軌道）已完成並呼叫 `prepareBuffer()` 利用瞬間的機會。
   * 將項目附加到 `MediaPlayer` 實例 `replaceCurrentItem()`。
   如果你打電話 `prepareBuffer()`，在 `onBufferPrepared` 處理程式。

1. 呼叫 `load` 的 `MediaPlayerItemLoader` 實例和傳遞要載入的資源，並可選地傳遞內容ID和 `MediaPlayerItemConfig` 實例。

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 要從流開頭以外的點進行緩衝，請調用 `prepareBuffer()` 開始緩衝的位置（以毫秒為單位）。
1. 使用 `replaceCurrentItem()` 和 `play()` 方法 `MediaPlayer` 從那開始演奏。
1. 等待空閒狀態和呼叫 `replaceCurrentItem`。
1. 播放項目。

   * 如果已載入但未緩衝該項：

      1. 等待初始化狀態。
      1. 呼叫 `prepareToPlay()`。
      1. 等待PREPARED狀態。
      1. 呼叫 `play()`。
   * 如果緩衝項：

      1. 等待緩衝區預準備事件。
      1. 呼叫 `play()`。
