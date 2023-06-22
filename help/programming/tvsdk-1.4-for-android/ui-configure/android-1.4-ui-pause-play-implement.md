---
description: 您可以新增TVSDK行為以暫停和播放按鈕。
title: 播放和暫停視訊
exl-id: 62e77f50-5133-4db5-bf10-fde7d28e959d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 播放和暫停視訊{#play-and-pause-a-video}

您可以新增TVSDK行為以暫停和播放按鈕。

1. 建立可執行以下動作的暫停/播放按鈕。
   1. 請等待播放器至少處於「已準備」狀態。
   1. 若要開始播放，請呼叫TVSDK播放方法：

      ```java
      void play() throws IllegalStateException;
      ```

   1. 若要暫停播放，請呼叫TVSDK暫停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 使用 `MediaPlayer.PlaybackEventListener.onStateChanged` 回撥以檢查錯誤或採取其他適當動作。

   在呼叫pause或play方法時，TVSDK會呼叫此回呼。 TVSDK會傳遞回呼中狀態變更的相關資訊，包括新狀態，例如PAUSED或PLAYING。
