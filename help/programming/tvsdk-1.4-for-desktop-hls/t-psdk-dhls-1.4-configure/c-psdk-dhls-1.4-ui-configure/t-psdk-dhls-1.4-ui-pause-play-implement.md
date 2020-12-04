---
description: 您可以新增TVSDK行為來暫停和播放按鈕。
seo-description: 您可以新增TVSDK行為來暫停和播放按鈕。
seo-title: 播放和暫停影片
title: 播放和暫停影片
uuid: 04b3b23f-5ef1-4cc4-a22f-f6ffa9cefce5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# 播放並暫停影片{#play-and-pause-a-video}

您可以新增TVSDK行為來暫停和播放按鈕。

1. 建立執行下列動作的暫停／播放按鈕。
   1. 等待您的播放器至少處於「已準備」狀態。
   1. 若要開始播放，請呼叫TVSDK播放方法：

      ```
      function play():void;
      ```

   1. 若要暫停播放，請呼叫TVSDK暫停方法：

      ```
      function pause():void;
      ```

1. 使用`MediaPlayerStatusChangeEvent.STATUS_CHANGED`事件的回呼來檢查錯誤或採取其他適當的動作。

   當呼叫pause或play方法時，TVSDK會呼叫此回呼。 TVSDK會傳遞回呼中狀態變更的相關資訊，包括新狀態，例如PAUSED或PLAYING。
