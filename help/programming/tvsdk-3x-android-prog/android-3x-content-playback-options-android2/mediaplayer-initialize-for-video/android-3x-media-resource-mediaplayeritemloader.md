---
description: 使用MediaPlayerItemLoader可協助您取得媒體資料流的相關資訊，而不需將MediaPlayer例項具現化。 這在預先緩衝資料流中特別有用，以便可以開始播放而不發生延遲。
title: 使用MediaPlayerItemLoader載入媒體資源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader載入媒體資源 {#load-a-media-resource-using-mediaplayeritemloader}

使用MediaPlayerItemLoader可協助您取得媒體資料流的相關資訊，而不需將MediaPlayer例項具現化。 這在預先緩衝資料流中特別有用，以便可以開始播放而不發生延遲。

此 `MediaPlayerItemLoader` 類別可協助您交換目前的媒體資源 `MediaPlayerItem` 而不將檢視附加至 `MediaPlayer` 執行個體，負責配置視訊解碼硬體資源。 受DRM保護的內容需要額外的步驟，但本手冊並未說明這些步驟。

>[!IMPORTANT]
>
>TVSDK不支援單一 `QoSProvider` 以使用兩者 `itemLoader` 和 `MediaPlayer`. 如果您的應用程式使用「立即開啟」，應用程式需要維護兩個 `QoS` 執行個體和管理兩個執行個體以取得資訊。 另請參閱 [即時開啟](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) 以取得詳細資訊。

1. 建立例項 `MediaPlayerItemLoader`.

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
   >建立單獨的例項 `MediaPlayerItemLoader` 用於每個資源。 不要使用一個 `MediaPlayerItemLoader` 執行個體以載入多個資源。

1. 實作 `ItemLoaderListener` 類別以接收來自的通知 `MediaPlayerItemLoader` 執行個體。

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

   在 `onLoadComplete()` callback，執行下列任一項作業：

   * 確認可能影響緩衝的任何專案（例如選取WebVTT或音軌）均已完成，並呼叫 `prepareBuffer()` 以利用立即啟用。
   * 將專案附加至 `MediaPlayer` 使用執行個體 `replaceCurrentItem()`.

   如果您呼叫 `prepareBuffer()`，您會在中收到BUFFER_PREPARED事件 `onBufferPrepared` 準備完成時的處理常式。
1. 呼叫 `load` 於 `MediaPlayerItemLoader` 例項並傳遞要載入的資源，以及選用的內容ID和 `MediaPlayerItemConfig` 執行個體。

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 若要從資料流開頭以外的點緩衝，請呼叫 `prepareBuffer()` 開始緩衝的位置（毫秒）。
1. 使用 `replaceCurrentItem()` 和 `play()` 方法 `MediaPlayer` 以開始播放。
1. 等候閒置狀態並呼叫 `replaceCurrentItem`.
1. 播放專案。

   * 如果專案已載入但未緩衝：

      1. 等待初始化的狀態。
      1. 呼叫 `prepareToPlay()`.
      1. 等候PREPARED狀態。
      1. 呼叫 `play()`.

   * 如果專案已緩衝：

      1. 等候緩衝準備好的事件。
      1. 呼叫 `play()`.
