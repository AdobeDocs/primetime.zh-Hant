---
description: 根據預設，開始播放時，VOD媒體從0開始，而即時媒體從使用者端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
title: 在特定時間輸入資料流
exl-id: 98688357-8394-4b62-b117-3ae2c5b0fecb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 在特定時間輸入資料流 {#enter-a-stream-at-a-specific-time}

根據預設，開始播放時，VOD媒體從0開始，而即時媒體從使用者端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。

1. 傳遞位置至 `MediaPlayer.prepareToPlay`.

   TVSDK會將給定位置視為資產的起點，且不需要搜尋操作。 如果位置不在可搜尋範圍內，TVSDK會使用預設位置。 如需詳細資訊，請參閱 [在媒體播放器中載入媒體資源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

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
