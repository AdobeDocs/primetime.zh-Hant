---
description: 當用戶快速前進或快速倒帶通過媒體時，他們處於特技播放模式。 要進入特技播放模式，您需要將MediaPlayer播放速率設定為1以外的值。
title: 快速前進和倒帶
exl-id: 58ed9a96-9617-4364-81d4-b404b23cf265
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 概述 {#implement-fast-forward-and-rewind-overview}

當用戶快速前進或快速倒帶通過媒體時，他們處於特技播放模式。 要進入特技播放模式，您需要將MediaPlayer播放速率設定為1以外的值。

要切換速度，必須設定一個值。

1. 通過設定正常播放模式(1x)上的速率，從特技播放模式移動到特技播放模式 `MediaPlayer` 值。

   * 的 `MediaPlayerItem` 類定義允許的播放速率。
   * 如果不允許指定速率，TVSDK將選擇最接近的允許速率。

   此示例將播放器的內部播放速率設定為請求的速率。

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

1. 您可以選擇偵聽匯率變動事件，這些事件會在您請求匯率變動時和實際發生匯率變動時通知您。

       TVSDK派送以下與特技播放相關的事件：
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 當 `rate` 值將更改為其他值。

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 以選定速率恢復播放時。

      當播放器從特技播放模式返回到正常播放模式時，TVSDK將調度這兩個事件。
