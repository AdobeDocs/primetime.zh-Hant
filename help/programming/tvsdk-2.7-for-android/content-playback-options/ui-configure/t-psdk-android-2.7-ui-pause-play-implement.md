---
description: 您可以新增暫停和播放按鈕來暫停或播放影片。
seo-description: 您可以新增暫停和播放按鈕來暫停或播放影片。
seo-title: 播放和暫停影片
title: 播放和暫停影片
uuid: 66fefead-7f1d-46ed-a23e-381f25697978
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 播放和暫停影片 {#play-and-pause-a-video}

您可以新增暫停和播放按鈕來暫停或播放影片。

1. 要建立暫停或播放按鈕：
   1. 等待玩家至少處於預備狀態。
   1. 若要開始播放，請呼叫 `play` 方法：

      ```java
      void play() throws MediaPlayerException;
      ```

   1. 若要暫停播放，請呼叫 `pause()` 方法：

      ```java
      void pause() throws MediaPlayerException;
      ```

1. 使用狀態變更的事件回呼來檢查錯誤或採取其他適當動作。

   TVSDK會呼叫此回呼 `pause()` 以取得 `play()` 或傳遞狀態變更的相關資訊，包括新狀態，例如暫停或播放。

