---
description: 建立處理HLS資料流設定和播放作業的PlaybackManager。 不需要其他設定。
title: 啟用視訊播放
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 啟用視訊播放 {#enable-video-playback}

建立處理HLS資料流設定和播放作業的PlaybackManager。 不需要其他設定。

1. 建立媒體播放器物件，確認下列程式碼存在於中 [!DNL PlayerFragment.java]：

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. 透過建立播放管理員 `ManagerFactory`：

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. 實作 `PlaybackManagerEventListener` 在 `PlayerFragment` 若要處理播放事件：

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. 在中登入事件監聽器 `PlayerFragment`：

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. 設定視訊資源：

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. 在中設定控制列作業 `PlayerFragment`：

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## 相關API檔案 {#related-api-documentation}

* [類別PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)
