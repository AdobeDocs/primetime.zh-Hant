---
description: 您可以保存視頻中的當前播放位置，並在將來的會話中在相同位置繼續播放。
title: 保存視頻位置，稍後繼續
exl-id: 9f6dc256-ee82-476d-96d0-f34b55f9e1f4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# 保存視頻位置，稍後繼續 {#save-the-video-position-and-resume-later}

您可以保存視頻中的當前播放位置，並在將來的會話中在相同位置繼續播放。

動態插入的廣告在用戶會話之間不同，因此保存位置 **與** 拼接廣告是指將來會話中的不同位置。 TVSDK提供了在忽略拼接廣告時檢索回放位置的方法。

1. 當用戶退出視頻時，應用程式將檢索並保存視頻中的位置。

   >[!TIP]
   >
   >不包括廣告持續時間。

   由於廣告模式、頻率封頂等原因，廣告中斷在每個會話中都可能會有所不同。 視頻在一個會話中的當前時間在未來會話中可能不同。 在視頻中保存位置時，應用程式將檢索本地時間，您可以將本地時間保存到設備上或伺服器上的資料庫中。

   例如，如果用戶在視頻的第20分鐘，而此位置包含5分鐘的廣告， `getCurrentTime` 將返回1200秒，而 `getLocalTime` 在這個位置會返回900秒。

   >[!IMPORTANT]
   >
   >即時/線性流的本地時間和當前時間相同。 在這個例子中， `convertToLocalTime` 沒有效果。 對於視頻點播，在播放廣告時，本地時間保持不變。

   ```java
   // Save the user session when player activity stops 
       @Override 
       public void onStop(){ 
           super.onStop(); 
           ... 
           prefs = PreferenceManager.getDefaultSharedPreferences( 
                                     getActivity().getApplicationContext()); 
           SharedPreferences.Editor editor = prefs.edit(); 
           // get the local time where stream stopped playing and  
           // save it in System preferences 
           editor.putLong(LAST_LOCAL_TIME, _mediaPlayer.getLocalTime());  
           editor.putString(LAST_MEDIA_RESOURCE, _contentInfo.toMediaResource().getUrl()); 
           editor.commit(); 
           ... 
       }
   ```

1. 播放器活動恢復時還原用戶會話。

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       ... 
       prefs =  
         PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil"). 
         equals(_contentInfo.toMediaResource().getUrl())) { 
           _lastKnownLocalTime =  
             prefs.getLong(LAST_LOCAL_TIME, 0); // get the last local time  
                                                // saved in system preferences 
           if(_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   ```

1. 要在同一位置恢復視頻：

   * 要從上次會話中保存的位置繼續播放視頻，請使用 `seekToLocalTime`。

      >[!TIP]
      >
      >此方法僅使用本地時間值調用。 如果使用當前時間結果調用方法，則會發生錯誤行為。

   * 要查找當前時間，請使用 `seek`。

1. 當您的應用程式收到 `onStatusChanged` 狀態更改事件，查找已保存的本地時間。

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if(_shouldResumePlayback){ 
               if(_lastKnownLocalTime >= 0) { 
                    _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
       ... 
   }
   ```

1. 提供在廣告策略介面中指定的廣告分段。
1. 通過擴展預設廣告策略選擇器來實現自定義廣告策略選擇器。
1. 通過實現，提供必須向用戶顯示的廣告分段 `selectAdBreaksToPlay`。

   該方法包括在局部時間位置之前的預卷和中卷和斷點。 您的應用程式可以決定播放預播廣告中斷，然後繼續到指定的本地時間，播放中播廣告中斷，然後繼續到指定的本地時間，或者不播放廣告中斷。
