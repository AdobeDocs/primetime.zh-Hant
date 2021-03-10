---
description: 依預設，當開始播放時，VOD媒體從0開始(MediaPlayer.LIVE_POINT)。 您可以覆寫預設行為。
title: 在特定時間輸入串流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%

---


# 在特定時間輸入流{#enter-a-stream-at-a-specific-time}

依預設，當開始播放時，VOD媒體從0開始(MediaPlayer.LIVE_POINT)。 您可以覆寫預設行為。

1. 將位置傳遞至`MediaPlayer.prepareToPlay`。

   TVSDK會將指定位置視為資產的起點。 不需要查找操作。 如果位置不在可檢視的範圍內，TVSDK會使用預設位置。

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

