---
description: 建立可處理HLS串流設定和播放作業的PlaybackManager。 不需要其他配置。
seo-description: 建立可處理HLS串流設定和播放作業的PlaybackManager。 不需要其他配置。
seo-title: 啟用視訊播放
title: 啟用視訊播放
uuid: ddc0defa-c40f-4ee6-a69f-d5eeca6c2fce
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# 啟用視訊播放 {#enable-video-playback}

建立可處理HLS串流設定和播放作業的PlaybackManager。 不需要其他配置。

1. 請確定下列程式碼存在於，以建立媒體播放器物件 [!DNL PlayerFragment.java]:

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. 透過下列項目建立播放管理 `ManagerFactory`器：

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. 實作 `PlaybackManagerEventListener` 中以 `PlayerFragment` 處理播放事件：

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. 在以下位置註冊事件偵聽器 `PlayerFragment`:

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. 設定視訊資源：

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. 在以下位置設定控制欄操作 `PlayerFragment`:

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## 相關API檔案 {#related-api-documentation}

* [Class PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)