---
description: 您可以新增暫停和播放按鈕來暫停或播放影片。
seo-description: 您可以新增暫停和播放按鈕來暫停或播放影片。
seo-title: 播放和暫停影片
title: 播放和暫停影片
uuid: 3778a1fb-929c-4579-a14c-561179473dea
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 播放並暫停影片{#play-and-pause-a-video}

您可以新增暫停和播放按鈕來暫停或播放影片。

1. 要建立暫停或播放按鈕：
   1. 等待玩家至少處於預備狀態。
   1. 若要開始播放，請呼叫`play`方法：

      ```java
      void play() throws MediaPlayerException;
      ```

   1. 若要暫停播放，請呼叫`pause()`方法：

      ```java
      void pause() throws MediaPlayerException;
      ```

1. 使用狀態變更的事件回呼來檢查錯誤或採取其他適當動作。

   TVSDK會針對`pause()`或`play()`呼叫此回呼，並傳遞有關狀態變更的資訊，包括新狀態，例如暫停或播放。