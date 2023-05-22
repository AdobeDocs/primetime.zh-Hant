---
description: 可以添加TVSDK行為以暫停和播放按鈕。
title: 播放並暫停視頻
exl-id: 62e77f50-5133-4db5-bf10-fde7d28e959d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 播放並暫停視頻{#play-and-pause-a-video}

可以添加TVSDK行為以暫停和播放按鈕。

1. 建立執行以下操作的暫停/播放按鈕。
   1. 等待玩家至少處於PREPARED狀態。
   1. 要開始播放，請調用TVSDK播放方法：

      ```java
      void play() throws IllegalStateException;
      ```

   1. 要暫停播放，請調用TVSDK暫停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 使用 `MediaPlayer.PlaybackEventListener.onStateChanged` 回調以檢查錯誤或採取其他適當操作。

   調用pause或play方法時，TVSDK將調用此回調。 TVSDK傳遞有關回調中狀態更改的資訊，包括新狀態，如PAUSED或PLAYING。
