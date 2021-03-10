---
description: 當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，請將MediaPlayer播放速率設為1以外的值。
title: 實作快速前進和倒退
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 概述{#implement-fast-forward-and-rewind}

當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，請將MediaPlayer播放速率設為1以外的值。

要切換速度，必須設定一個值。

1. 將`MediaPlayer`上的速率設為允許的值，從一般播放模式(1x)移至特技播放模式。

       請記住下列資訊：
   
   * `MediaPlayerItem`類別定義允許的播放速率。
   * 如果不允許指定速率，TVSDK會選取最接近的允許速率。

      下列範例將播放器的內部播放速率設定為請求的速率：

      ```
      import com.adobe.mediacore.MediaPlayer; 
      import com.adobe.mediacore.MediaPlayerItem; 
      import com.adobe.mediacore.MediaPlayerException; 
      import java.util.List; 
      import java.lang.Float; 
      
      private boolean setPlaybackRate(MediaPlayer player, float rate)  
        throws MediaPlayerException { 
          // Get list of playback rates that the media player supports 
          MediaPlayerItem item = player.getCurrentItem(); 
          if (item == null) return false; 
          List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
      
          // Return false if requested rate is not supported 
          if (availableRates.indexOf(rate) == -1) return false; 
      
          // Otherwise set the playback rate to the requested rate  
          // (this can throw MediaPlayerException) 
          player.setRate(rate); 
          return true; 
      }
      ```

1. 您可以選擇性地監聽費率變動事件，這些事件會在您請求費率變動時以及實際發生費率變動時通知您。

TVSDK會記錄下列與特技播放相關的事件：

* `MediaPlayerEvent.RATE_SELECTED`，當值變 `rate` 更為不同值時。

* `MediaPlayerEvent.RATE_PLAYING`，當播放以選取的速率繼續時。

   當播放器從特技播放模式返回正常播放模式時，TVSDK會調度這些事件。