---
description: 可以添加瀏覽器TVSDK行為以暫停和播放按鈕。
title: 播放並暫停視頻
exl-id: ce3f8b0c-9765-4e77-b096-6b9789608fa8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 播放並暫停視頻{#play-and-pause-a-video}

可以添加瀏覽器TVSDK行為以暫停和播放按鈕。

1. 建立執行以下操作的暫停/播放按鈕。
   1. 等待玩家至少處於PREPARED狀態。
   1. 要開始播放，請調用瀏覽器TVSDK播放方法：

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. 要暫停播放，請調用瀏覽器TVSDK暫停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 聽著 `AdobePSDK.MediaPlayerStatusChangeEvent` 事件，檢查錯誤或執行其他相應操作。

   當調用暫停或播放方法時，瀏覽器TVSDK會觸發此事件並傳遞有關事件對象的資訊，包括新狀態，如 `MediaPlayerStatus.PLAYING` 或 `MediaPlayerStatus.PAUSED`。
