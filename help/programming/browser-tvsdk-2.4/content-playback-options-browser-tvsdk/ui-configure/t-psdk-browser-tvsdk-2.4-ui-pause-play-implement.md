---
description: 您可以新增瀏覽器TVSDK行為以暫停和播放按鈕。
title: 播放和暫停視訊
exl-id: ce3f8b0c-9765-4e77-b096-6b9789608fa8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 播放和暫停視訊{#play-and-pause-a-video}

您可以新增瀏覽器TVSDK行為以暫停和播放按鈕。

1. 建立可執行以下動作的暫停/播放按鈕。
   1. 請等待播放器至少處於「已準備」狀態。
   1. 若要開始播放，請呼叫瀏覽器TVSDK播放方法：

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. 若要暫停播放，請呼叫瀏覽器TVSDK暫停方法：

      ```java
      void pause() throws IllegalStateException;
      ```

1. 聆聽 `AdobePSDK.MediaPlayerStatusChangeEvent` 事件，以檢查錯誤或採取其他適當的動作。

   呼叫暫停或播放方法並傳遞事件物件的相關資訊(包括新狀態，例如 `MediaPlayerStatus.PLAYING` 或 `MediaPlayerStatus.PAUSED`.
