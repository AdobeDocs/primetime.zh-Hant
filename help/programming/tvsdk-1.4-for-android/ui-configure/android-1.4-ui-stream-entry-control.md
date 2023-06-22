---
description: 根據預設，開始播放時，VOD媒體從0 (MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
title: 在特定時間輸入資料流
exl-id: a16b6281-37d5-491c-a2d0-2090894c8a70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 在特定時間輸入資料流 {#enter-a-stream-at-a-specific-time}

根據預設，開始播放時，VOD媒體從0 (MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。

1. 傳遞位置至 `MediaPlayer.prepareToPlay`.

   TVSDK會將指定位置視為資產的起點。 不需要搜尋作業。 如果位置不在可搜尋範圍內，TVSDK會使用預設位置。

   例如：

   ```java
   long desiredPostion = //TODO : choose a value; 
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
               case PREPARING: 
               showBufferingSpinner(); 
               break; 
           ... 
       } 
   } 
   ```
