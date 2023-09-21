---
description: 根據預設，開始播放時，VOD媒體從0開始，即時媒體從使用者端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
title: 在特定時間輸入資料流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 在特定時間輸入資料流 {#enter-a-stream-at-a-specific-time}

根據預設，開始播放時，VOD媒體從0開始，即時媒體從使用者端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。

1. 傳遞位置至 `MediaPlayer.prepareToPlay`.

   TVSDK會將給定位置視為資產的起點，且不需要搜尋作業。 如果位置不在可搜尋範圍內，TVSDK會使用預設位置。 如需詳細資訊，請參閱 [在媒體播放器中載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

   例如：

   ```java
   long desiredPostion = // TODO : choose a value; 
   @Override 
   public void onStatusChanged(MediaPlayerStatusChangedEvent statusChangedEvent) {   
       switch (statusChangedEvent.getStatus()) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
           case PREPARING: 
               showBufferingSpinner(); 
               break; 
       } 
   }
   ```
