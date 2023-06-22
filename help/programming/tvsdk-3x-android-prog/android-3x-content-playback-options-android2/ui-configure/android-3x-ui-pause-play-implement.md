---
description: 您可以新增暫停和播放按鈕來暫停或播放視訊。
title: 播放和暫停視訊
exl-id: 7084ef55-4da6-48af-9951-5360bad7bfa9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 播放和暫停視訊 {#play-and-pause-a-video}

您可以新增暫停和播放按鈕來暫停或播放視訊。

1. 若要建立暫停或播放按鈕：
   1. 等候播放器至少處於準備狀態。
   1. 若要開始播放，請呼叫 `play` 方法：

      ```java
      void play() throws MediaPlayerException;
      ```

   1. 若要暫停播放，請呼叫 `pause()` 方法：

      ```java
      void pause() throws MediaPlayerException;
      ```

1. 使用狀態變更事件回呼來檢查錯誤或採取其他適當的動作。

   TVSDK呼叫此回呼 `pause()` 或 `play()` 和會傳遞有關狀態變更的資訊，包括新狀態，例如暫停或播放。
