---
description: 依預設，當播放開始時，VOD媒體從0開始，而即時媒體從使用者端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
title: 在特定時間輸入資料流
exl-id: 2fb361c1-7133-4e17-a12b-e11f6f7c5479
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 在特定時間輸入資料流{#enter-a-stream-at-a-specific-time}

依預設，當播放開始時，VOD媒體從0開始，而即時媒體從使用者端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。

1. 傳遞位置至 `MediaPlayer.prepareToPlay`.
1. 瀏覽器TVSDK會使用此位置作為資產的起點。

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
