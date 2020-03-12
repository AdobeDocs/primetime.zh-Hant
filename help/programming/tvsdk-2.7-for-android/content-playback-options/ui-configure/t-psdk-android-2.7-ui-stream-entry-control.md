---
description: 依預設，當開始播放時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
seo-description: 依預設，當開始播放時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。
seo-title: 在特定時間輸入串流
title: 在特定時間輸入串流
uuid: 65a19192-b890-4d69-9cb1-582a22988d2b
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# 在特定時間輸入串流 {#enter-a-stream-at-a-specific-time}

依預設，當開始播放時，VOD媒體從0開始，而即時媒體從用戶端即時點(MediaPlayer.LIVE_POINT)開始。 您可以覆寫預設行為。

1. 將位置傳遞至 `MediaPlayer.prepareToPlay`。

   TVSDK會將指定位置視為資產的起點，而不需要搜尋作業。 如果位置不在可檢視的範圍內，TVSDK會使用預設位置。 如需詳細資訊，請 [參閱在媒體播放器中載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md)。

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

