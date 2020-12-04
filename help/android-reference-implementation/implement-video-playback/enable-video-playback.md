---
description: 建立可處理HLS串流設定和播放作業的PlaybackManager。 不需要其他配置。
seo-description: 建立可處理HLS串流設定和播放作業的PlaybackManager。 不需要其他配置。
seo-title: 啟用視訊播放
title: 啟用視訊播放
uuid: ddc0defa-c40f-4ee6-a69f-d5eeca6c2fce
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# 啟用視頻播放{#enable-video-playback}

建立可處理HLS串流設定和播放作業的PlaybackManager。 不需要其他配置。

1. 請確定[!DNL PlayerFragment.java]中存在以下代碼，以建立媒體播放器對象：

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. 通過`ManagerFactory`建立播放管理器：

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. 在`PlayerFragment`中實作`PlaybackManagerEventListener`以處理播放事件：

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. 在`PlayerFragment`中註冊事件偵聽器：

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. 設定視訊資源：

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. 在`PlayerFragment`中設定控制欄操作：

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## 相關API檔案{#related-api-documentation}

* [Class PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)