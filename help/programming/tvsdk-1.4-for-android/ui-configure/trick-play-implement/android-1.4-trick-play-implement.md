---
description: 當使用者在媒體中快速前進或快速倒帶時，他們處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。
title: 實作快速前進和倒帶
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 概觀 {#implement-fast-forward-and-rewind-overview}

當使用者在媒體中快速前進或快速倒帶時，他們處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。

若要切換速度，您必須設定一個值。

1. 從一般播放模式(1x)移至特技播放模式，方法是在 `MediaPlayer` 至允許的值。

   * 此 `MediaPlayerItem` 類別會定義允許的播放速率。
   * 如果不允許指定的速率，TVSDK會選取最接近的允許速率。

   此範例將播放器的內部播放速率設定為要求的速率。

   ```java
   import com.adobe.mediacore.MediaPlayer; 
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerException; 
   import java.util.List; 
   import java.lang.Float; 
   
   private boolean setPlaybackRate(MediaPlayer player, float rate) throws MediaPlayerException  
   { 
       //Get list of playback rates that the media player supports 
       MediaPlayerItem item = player.getCurrentItem(); 
       if(item == null) return false; 
       List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
   
       //Return false if requested rate is not supported 
       if(availableRates.indexOf(rate) == -1) return false; 
   
       //Otherwise set the playback rate to the requested rate  
       //(this can throw MediaPlayerException) 
       player.setRate(rate); 
       return true; 
   }
   ```

1. 您可以選擇接聽費率變更事件，讓您知道何時要求費率變更，以及實際發生費率變更的時間。

       TVSDK會傳送下列與特技播放相關的事件：
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 當 `rate` 值會變更為其他值。

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 以選取的速率繼續播放時。

     當播放器從特技播放模式返回正常播放模式時，TVSDK會傳送這兩個事件。
