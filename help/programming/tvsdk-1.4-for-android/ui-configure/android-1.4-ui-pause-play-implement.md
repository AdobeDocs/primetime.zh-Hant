---
description: 您可以新增TVSDK行為來暫停和播放按鈕。
seo-description: 您可以新增TVSDK行為來暫停和播放按鈕。
seo-title: 播放和暫停影片
title: 播放和暫停影片
uuid: 24b26364-5cb8-4a95-9574-cc52ddfa876b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 播放和暫停影片{#play-and-pause-a-video}

您可以新增TVSDK行為來暫停和播放按鈕。

1. 建立執行下列動作的暫停／播放按鈕。
   1. 等待您的播放器至少處於「已準備」狀態。
   1. 若要開始播放，請呼叫TVSDK播放方法：

      ```java
      void play() throws IllegalStateException;
      ```

   1. 若要暫停播放，請呼叫TVSDK暫停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 使用回 `MediaPlayer.PlaybackEventListener.onStateChanged` 呼來檢查錯誤或採取其他適當的動作。

   當呼叫pause或play方法時，TVSDK會呼叫此回呼。 TVSDK會傳遞回呼中狀態變更的相關資訊，包括新狀態，例如PAUSED或PLAYING。

