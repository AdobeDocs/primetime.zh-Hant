---
description: 根據預設，當播放開始時，VOD媒體從0開始，而即時媒體從使用者端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
title: 在特定時間輸入資料流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 在特定時間輸入資料流{#enter-a-stream-at-a-specific-time}

根據預設，當播放開始時，VOD媒體從0開始，而即時媒體從使用者端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。

1. 傳遞位置至 `MediaPlayer.prepareToPlay`.
1. 瀏覽器TVSDK會以此位置作為資產的起點。

   >[!NOTE]
   >
   >不需要搜尋作業。

1. 如果位置不在可搜尋範圍內，則會使用預設位置。

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
