---
description: 您可以儲存視訊中目前的播放位置，並在未來作業中在相同位置繼續播放。
seo-description: 您可以儲存視訊中目前的播放位置，並在未來作業中在相同位置繼續播放。
seo-title: 儲存視訊位置並稍後繼續
title: 儲存視訊位置並稍後繼續
uuid: 322f780d-09ba-44b0-b2e5-46288bf58fda
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 儲存視訊位置並稍後繼續 {#save-the-video-position-and-resume-later}

您可以儲存視訊中目前的播放位置，並在未來作業中在相同位置繼續播放。

動態插入的廣告在使用者工作階段間不同，因此 **使用拼接** 的廣告來儲存位置，是指未來工作階段中的不同位置。 TVSDK提供在忽略拼接廣告時擷取播放位置的方法。

1. 當使用者結束視訊時，您的應用程式會擷取並儲存視訊中的位置。

   >[!TIP]
   >
   >廣告期間不包含在內。

   由於廣告模式、頻率上限設定等原因，每個工作階段的廣告插播都會有所不同。 視訊在某個作業中的目前時間在未來作業中可能不同。 在視訊中儲存位置時，應用程式會擷取本機時間，您可將它儲存在裝置上或伺服器的資料庫中。

   例如，如果使用者是視訊的第20分鐘，而此位置包含5分鐘廣告，則 `getCurrentTime` 會傳回1200秒，而 `getLocalTime` 此位置則傳回900秒。

   >[!IMPORTANT]
   >
   >即時／線性串流的本機時間與目前時間相同。 在這種情況下， `convertToLocalTime` 沒有作用。 對於VOD，當廣告播放時，當地時間保持不變。

   ```java
   // Save the user session when player activity stops 
   @Override 
   public void onStop() { 
       super.onStop(); 
       ... 
       prefs = PreferenceManager.getDefaultSharedPreferences( 
                 getActivity().getApplicationContext() 
               ); 
       SharedPreferences.Editor editor = prefs.edit(); 
       // get the local time where stream stopped playing and  
       // save it in System preferences 
       editor.putLong(LAST_LOCAL_TIME, _mediaPlayer.getLocalTime());  
       editor.putString(LAST_MEDIA_RESOURCE, _contentInfo.toMediaResource().getUrl()); 
       editor.commit(); 
       ... 
   } 
   ```

1. 當播放器活動繼續時，還原使用者工作階段。

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       ... 
       prefs = PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil").equals(_contentInfo.toMediaResource().getUrl())) { 
   
           _lastKnownLocalTime = prefs.getLong(LAST_LOCAL_TIME, 0);    // get the last local time saved  
                                                                       // in system preferences 
           if (_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   ```

1. 要在相同位置繼續視頻：

   * 若要從先前作業儲存的位置繼續播放視訊，請使用 `seekToLocalTime`。

      >[!TIP]
      >
      >此方法僅與本機時間值一起呼叫。 如果以目前的時間結果呼叫方法，就會發生錯誤行為。

   * 若要尋找目前的時間，請使用 `seek`。

1. 當您的應用程式收到狀 `onStatusChanged` 態變更事件時，請尋找儲存的本機時間。

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if (_shouldResumePlayback) { 
               if(_lastKnownLocalTime >= 0) { 
                   _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
        ... 
   } 
   ```

1. 依照廣告原則介面中的指定，提供廣告分段。
1. 延伸預設廣告原則選擇器，以實作自訂廣告原則選擇器。
1. 透過實作，提供必須向使用者呈現的廣告插頁 `selectAdBreaksToPlay`。

   此方法包括前段廣告插播和中段廣告插播，前段廣告插播於本機時間位置。 您的應用程式可決定播放前段廣告插播並繼續到指定的當地時間、播放中段廣告插播並繼續到指定的當地時間，或不播放廣告插播。
