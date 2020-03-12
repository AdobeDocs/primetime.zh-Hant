---
description: 依預設，當播放開始時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
seo-description: 依預設，當播放開始時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
seo-title: 在特定時間輸入串流
title: 在特定時間輸入串流
uuid: 5db73b50-0629-4fb1-8f12-6c88e4cd7109
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 在特定時間輸入串流{#enter-a-stream-at-a-specific-time}

依預設，當播放開始時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。

1. 將位置傳遞至 `MediaPlayer.prepareToPlay`。
1. 瀏覽器TVSDK會將此位置作為資產的起點。

   >[!NOTE]
   >
   >不需要查找操作。

1. 如果位置不在可查找範圍內，則使用預設位置。

   例如：

   ```js
   var desiredPostion = //choose a value; 
   onStatusChange = function (event) { 
       case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
           console.log("Player Status: INITIALIZED"); 
           player.prepareToPlay(desiredPostion); 
           break; 
   } 
   ```

