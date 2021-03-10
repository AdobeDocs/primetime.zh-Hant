---
description: 使用MediaPlayerItemLoader可協助您取得媒體串流的相關資訊，而不需執行個體化MediaPlayer例項。 這在預緩衝流中特別有用，以便可以無延遲地開始播放。
title: 使用MediaPlayerItemLoader載入媒體資源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# 使用MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}載入媒體資源

使用MediaPlayerItemLoader可協助您取得媒體串流的相關資訊，而不需執行個體化MediaPlayer例項。 這在預緩衝流中特別有用，以便可以無延遲地開始播放。

`MediaPlayerItemLoader`類別可協助您交換目前`MediaPlayerItem`的媒體資源，而不需將檢視附加到`MediaPlayer`例項，以分配視訊解碼硬體資源。 DRM保護內容需要其他步驟，但本手冊並未說明這些步驟。

>[!IMPORTANT]
>
>TVSDK不支援單一`QoSProvider`搭配`itemLoader`和`MediaPlayer`使用。 如果您的應用程式使用Instant On，則應用程式需要維護兩個`QoS`例項，並管理這兩個例項的資訊。 如需詳細資訊，請參閱[Instant-on](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md)。

1. 建立`MediaPlayerItemLoader`實例。

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
   >為每個資源建立一個單獨的`MediaPlayerItemLoader`實例。 請勿使用一個`MediaPlayerItemLoader`實例來載入多個資源。

1. 實作`ItemLoaderListener`類別，以接收來自`MediaPlayerItemLoader`例項的通知。

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

   在`onLoadComplete()`回呼中，執行下列任一項作業：

   * 請確定任何可能影響緩衝的項目（例如，選取WebVTT或音軌）皆已完成，並呼叫`prepareBuffer()`以立即啟動。
   * 使用`replaceCurrentItem()`將項目附加到`MediaPlayer`實例。

   如果調用`prepareBuffer()`，則在準備完成時，將在`onBufferPrepared`處理程式中收到BUFFER_PREPARED事件。
1. 在`MediaPlayerItemLoader`實例上調用`load`並傳遞要載入的資源，以及（可選）內容ID和`MediaPlayerItemConfig`實例。

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 要從流開頭以外的點進行緩衝，請調用`prepareBuffer()`，其位置（以毫秒為單位）為啟動緩衝。
1. 使用`replaceCurrentItem()`和`play()`方法，從此開始播放。`MediaPlayer`
1. 等待空閒狀態並調用`replaceCurrentItem`。
1. 播放項目。

   * 如果項目已載入但未緩衝：

      1. 等待初始化狀態。
      1. 呼叫`prepareToPlay()`。
      1. 等待PREPARED狀態。
      1. 呼叫`play()`。
   * 如果項目是緩衝的：

      1. 等待緩衝區預準備事件。
      1. 呼叫`play()`。