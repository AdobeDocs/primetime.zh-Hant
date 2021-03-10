---
description: 依預設，當播放開始時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
title: 在特定時間輸入串流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---


# 在特定時間輸入串流{#enter-a-stream-at-a-specific-time}

依預設，當播放開始時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。

1. 將位置傳遞至`MediaPlayer.prepareToPlay`。
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

