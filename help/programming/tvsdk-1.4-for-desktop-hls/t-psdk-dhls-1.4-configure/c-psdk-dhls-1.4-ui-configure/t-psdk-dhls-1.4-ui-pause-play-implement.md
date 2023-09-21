---
description: 您可以新增TVSDK行為以暫停和播放按鈕。
title: 播放和暫停視訊
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 播放和暫停視訊{#play-and-pause-a-video}

您可以新增TVSDK行為以暫停和播放按鈕。

1. 建立可執行以下動作的暫停/播放按鈕。
   1. 請等候您的播放器至少處於「已準備」狀態。
   1. 若要開始播放，請呼叫TVSDK播放方法：

      ```
      function play():void;
      ```

   1. 若要暫停播放，請呼叫TVSDK暫停方法：

      ```
      function pause():void;
      ```

1. 使用回撥至 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 事件，以檢查錯誤或採取其他適當動作。

   在呼叫pause或play方法時，TVSDK會呼叫此回呼。 TVSDK會傳遞回呼中狀態變更的相關資訊，包括新狀態，例如「已暫停」或「正在播放」。
