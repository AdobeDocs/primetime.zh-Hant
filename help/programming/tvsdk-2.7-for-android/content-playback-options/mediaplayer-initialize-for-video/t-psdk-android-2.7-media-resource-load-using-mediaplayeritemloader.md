---
description: 使用MediaPlayerItemLoader可協助您取得媒體串流的相關資訊，而不需執行個體化MediaPlayer例項。 這在預緩衝流中特別有用，以便可以無延遲地開始播放。
seo-description: 使用MediaPlayerItemLoader可協助您取得媒體串流的相關資訊，而不需執行個體化MediaPlayer例項。 這在預緩衝流中特別有用，以便可以無延遲地開始播放。
seo-title: 使用MediaPlayerItemLoader載入媒體資源
title: 使用MediaPlayerItemLoader載入媒體資源
uuid: 43ca2470-1fd2-4f66-94fe-a12ed17b52d7
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# 使用MediaPlayerItemLoader載入媒體資源 {#load-a-media-resource-using-mediaplayeritemloader}

使用MediaPlayerItemLoader可協助您取得媒體串流的相關資訊，而不需執行個體化MediaPlayer例項。 這在預緩衝流中特別有用，以便可以無延遲地開始播放。

該類 `MediaPlayerItemLoader` 別可協助您交換目前的媒體資源，而 `MediaPlayerItem` 不需將檢視附加至例項， `MediaPlayer` 以分配視訊解碼硬體資源。 DRM保護內容需要其他步驟，但本手冊並未說明這些步驟。

>[!IMPORTANT]
>
>TVSDK不支援單一軟體 `QoSProvider` 搭配和 `itemLoader` 運作 `MediaPlayer`。 如果您的應用程式使用「立即啟動」，應用程式需要維護兩個例項， `QoS` 並管理這兩個例項以取得相關資訊。 如需 [詳細資訊](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) ，請參閱立即啟動。

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
   >為每個資源建立單 `MediaPlayerItemLoader` 獨的實例。 請勿使用一個例 `MediaPlayerItemLoader` 項來載入多個資源。

1. 實作類 `ItemLoaderListener` 別以接收來自例項的 `MediaPlayerItemLoader` 通知。

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

   在回呼 `onLoadComplete()` 中，執行下列其中一項作業：

   * 請確定任何可能影響緩衝的項目（例如選取WebVTT或音軌）皆已完成，並 `prepareBuffer()` 呼叫以立即啟動。
   * 使用將項目附加 `MediaPlayer` 到實例 `replaceCurrentItem()`。
   如果調用 `prepareBuffer()`，則在準備完成時，將在處理程式 `onBufferPrepared` 中收到BUFFER_PREPARED事件。

1. 呼 `load` 叫實 `MediaPlayerItemLoader` 例並傳遞要載入的資源，可選擇內容ID和實 `MediaPlayerItemConfig` 例。

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 要從流開頭以外的點進行緩衝，請調 `prepareBuffer()` 用要開始緩衝的位置（以毫秒為單位）。
1. 使用 `replaceCurrentItem()` 和 `play()` 方 `MediaPlayer` 法開始播放。
1. 等待空閒狀態和呼叫 `replaceCurrentItem`。
1. 播放項目。

   * 如果項目已載入但未緩衝：

      1. 等待初始化狀態。
      1. 打 `prepareToPlay()`電話。
      1. 等待PREPARED狀態。
      1. 打 `play()`電話。
   * 如果項目是緩衝的：

      1. 等待緩衝區預準備事件。
      1. 打 `play()`電話。