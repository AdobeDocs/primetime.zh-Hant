---
description: 您可以新增瀏覽器TVSDK行為以暫停和播放按鈕。
title: 播放和暫停視訊
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 播放和暫停視訊{#play-and-pause-a-video}

您可以新增瀏覽器TVSDK行為以暫停和播放按鈕。

1. 建立可執行以下動作的暫停/播放按鈕。
   1. 請等候播放器至少處於「已準備」狀態。
   1. 若要開始播放，請呼叫瀏覽器TVSDK播放方法：

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. 若要暫停播放，請呼叫瀏覽器TVSDK暫停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 聆聽 `AdobePSDK.MediaPlayerStatusChangeEvent` 事件，以檢查錯誤或採取其他適當動作。

   呼叫暫停或播放方法時，瀏覽器TVSDK會觸發此事件，並傳遞有關事件物件的資訊，包括新狀態，例如 `MediaPlayerStatus.PLAYING` 或 `MediaPlayerStatus.PAUSED`.
