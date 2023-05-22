---
description: 您可以添加暫停和播放按鈕來暫停或播放視頻。
title: 播放並暫停視頻
exl-id: 7084ef55-4da6-48af-9951-5360bad7bfa9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 播放並暫停視頻 {#play-and-pause-a-video}

您可以添加暫停和播放按鈕來暫停或播放視頻。

1. 要建立暫停或播放按鈕：
   1. 等待玩家至少處於準備狀態。
   1. 要開始播放，請調用 `play` 方法：

      ```java
      void play() throws MediaPlayerException;
      ```

   1. 要暫停播放，請調用 `pause()` 方法：

      ```java
      void pause() throws MediaPlayerException;
      ```

1. 使用狀態更改的事件回調檢查錯誤或採取其他適當的操作。

   TVSDK調用此回調 `pause()` 或 `play()` 並傳遞有關狀態更改的資訊，包括新狀態，如暫停或播放。
