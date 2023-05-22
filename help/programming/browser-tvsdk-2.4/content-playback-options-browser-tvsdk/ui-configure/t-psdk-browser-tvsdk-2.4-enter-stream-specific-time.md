---
description: 預設情況下，當播放開始時，VOD媒體從0開始，而即時媒體從客戶端即時點(MediaPlayer.LIVE_POINT)開始。 可以覆蓋預設行為。
title: 在特定時間輸入流
exl-id: 2fb361c1-7133-4e17-a12b-e11f6f7c5479
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 在特定時間輸入流{#enter-a-stream-at-a-specific-time}

預設情況下，當播放開始時，VOD媒體從0開始，而即時媒體從客戶端即時點(MediaPlayer.LIVE_POINT)開始。 可以覆蓋預設行為。

1. 將位置傳遞到 `MediaPlayer.prepareToPlay`。
1. 瀏覽器TVSDK將此位置用作資產的起點。

   >[!NOTE]
   >
   >不需要查找操作。

1. 如果位置不在可瀏覽範圍內，則使用預設位置。

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
