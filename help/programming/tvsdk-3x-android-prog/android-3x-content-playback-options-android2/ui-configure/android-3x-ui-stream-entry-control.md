---
description: 依預設，當開始播放時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
seo-description: 依預設，當開始播放時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
seo-title: 在特定時間輸入串流
title: 在特定時間輸入串流
uuid: b315a967-77ad-4352-8a32-f228704d4b20
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# 在特定時間輸入串流 {#enter-a-stream-at-a-specific-time}

依預設，當開始播放時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。

1. 將位置傳遞至 `MediaPlayer.prepareToPlay`。

   TVSDK會將指定位置視為資產的起點，而不需要搜尋作業。 如果位置不在可檢視的範圍內，TVSDK會使用預設位置。 如需詳細資訊，請 [參閱在媒體播放器中載入媒體資源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md)。

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
