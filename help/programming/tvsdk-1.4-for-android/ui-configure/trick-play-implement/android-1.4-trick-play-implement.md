---
description: 當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。
seo-description: 當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。
seo-title: 實作快速前進和倒退
title: 實作快速前進和倒退
uuid: 2e5d0fd0-0290-4f08-b9c6-c8ecde26abb8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 概述{#implement-fast-forward-and-rewind-overview}

當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。

要切換速度，必須設定一個值。

1. 將`MediaPlayer`上的速率設為允許的值，從一般播放模式(1x)移至特技播放模式。

   * `MediaPlayerItem`類別定義允許的播放速率。
   * 如果不允許指定速率，TVSDK會選取最接近的允許速率。

   此範例會將播放器的內部播放速率設為要求的速率。

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

1. 您可以選擇性地監聽費率變動事件，這些事件會在您請求費率變動時以及實際發生費率變動時告知您。

       TVSDK記錄下列與特技播放相關的事件：
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 值變 `rate` 更為不同的值時。

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 當播放以選取的速率繼續時。

      當播放器從特技播放模式返回正常播放模式時，TVSDK會調度這兩個事件。

