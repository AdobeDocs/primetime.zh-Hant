---
description: 您可以新增瀏覽器TVSDK行為來暫停和播放按鈕。
title: 播放和暫停影片
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 播放並暫停影片{#play-and-pause-a-video}

您可以新增瀏覽器TVSDK行為來暫停和播放按鈕。

1. 建立執行下列動作的暫停／播放按鈕。
   1. 等待您的播放器至少處於「已準備」狀態。
   1. 若要開始播放，請呼叫瀏覽器TVSDK播放方法：

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. 若要暫停播放，請呼叫瀏覽器TVSDK暫停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 監聽`AdobePSDK.MediaPlayerStatusChangeEvent`事件以檢查錯誤或採取其他適當動作。

   當呼叫暫停或播放方法並傳遞事件物件的相關資訊（包括新狀態，例如`MediaPlayerStatus.PLAYING`或`MediaPlayerStatus.PAUSED`）時，瀏覽器TVSDK會觸發此事件。

