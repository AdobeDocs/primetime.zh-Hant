---
description: 當裝置螢幕關閉且必須由您的應用程式處理時，暫停並還原TVSDK MediaPlayer。
keywords: SurfaceView;Suspend;Restore;BroadcastReceiver
seo-description: 當裝置螢幕關閉且必須由您的應用程式處理時，暫停並還原TVSDK MediaPlayer。
seo-title: 暫停和還原MediaPlayer
title: 暫停和還原MediaPlayer
uuid: 624a87df-df65-4358-915b-c09a3a4fa224
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 暫停和還原MediaPlayer {#suspend-and-restore-mediaplayer}

當裝置螢幕關閉且必須由您的應用程式處理時，暫停並還原TVSDK MediaPlayer。

您可以在Android廣播接收器內處 `MediaPlayer` 理暫停和還原操作，以進行畫面開啟／關閉。

TVSDK無法判斷片段（或活動）是何時在背景或前景。 此外，當裝置畫 `SurfaceView` 面關閉時（但活動已暫停）,Android不會毀損。 不過，當 `SurfaceView` 裝置 *將您的應用程式置於背景時* ，會遭到銷毀。 TVSDK無法偵測這些變更，因此必須由您的應用程式處理。

下列范常式式碼，說明當裝置畫面在應用程式層級開啟或關閉 `MediaPlayer` 時，應用程式如何處理暫停和復原：

```java
// Track the state of a fragment to determine if it is PAUSED or RESUMED 
private boolean isActivityPaused = false; 
 
/** 
* Register the broadcast receiver to track screen on/screen off functions triggered from 
device. 
*/ 
private BroadcastReceiver mReceiver = new BroadcastReceiver() { 
    @Override 
    public void onReceive(Context context, Intent intent) { 
 
        // Call suspend when screen is turned off and mediaPlayer is not null and 
        // mediaplayer status is not suspended/Error/Released state. 
        if (intent.getAction().equals(Intent.ACTION_SCREEN_OFF)) { 
            try { 
                if (mediaPlayer != null && 
                  lastKnownStatus != MediaPlayerStatus.ERROR && 
                  lastKnownStatus != MediaPlayerStatus.RELEASED && 
                  lastKnownStatus != MediaPlayerStatus.SUSPENDED) { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOff:", 
                    "Suspending mediaplayer as screen is turned off and mediaPlayer 
                    status is " + lastKnownStatus.toString()); 
                    mediaPlayer.suspend(); 
                } 
                else { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOff:", 
                      "Not suspending mediaplayer since mediaplayer status is " 
                      + lastKnownStatus.toString()); 
                } 
            } catch(MediaPlayerException e) { 
                PrimetimeReference.logger.e(LOG_TAG+"#screenOff:", 
                  "MediaPlayer Exception for suspend() call"); 
            } 
        } 
        else if (intent.getAction().equals(Intent.ACTION_SCREEN_ON)) { 
            // Call restore when the screen is turned on and mediaplayer is not in the  
            // suspended status.  This is for the screen on condition when the device  
            // does not have a lock and turning on the screen immediately brings the  
            // fragment to the foreground. 
            try { 
                if(lastKnownStatus == MediaPlayerStatus.SUSPENDED && !isActivityPaused) { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOn:", 
                      "Restoring mediaplayer since screen is turned on and mediaPlayer status is " 
                      + lastKnownStatus.toString()); 
                    mediaPlayer.restore(); 
                } 
                else { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOn:", 
                      "Not restoring mediaplayer since mediaPlayer status is " 
                      + lastKnownStatus.toString()); 
                } 
            } catch(MediaPlayerException e) { 
                PrimetimeReference.logger.e(LOG_TAG+"#screenOn:", 
                  "MediaPlayer Exception for restore() call"); 
            } 
        } 
    } 
}; 
 
/* 
* Activity or Fragment's onPause() overridden method 
*/ 
@Override 
public void onPause() { 
    PrimetimeReference.logger.i(LOG_TAG + "#onPause", "Player activity paused."); 
 
    // Set the fragment paused status to true when app goes in background. 
    isActivityPaused = true; 
    super.onPause(); 
} 
 
/* 
* Activity or Fragment's onResume() overridden method 
*/ 
@Override 
public void onResume() { 
    super.onResume(); 
 
    /** 
    * When the device has a lock/pin the on resume will be called only after the device 
      is unlocked. 
    * Screen on does not call the onResume() method so we need to handle restore here 
      explicitly. 
    */ 
    if(lastKnownStatus == MediaPlayerStatus.SUSPENDED && isActivityPaused) { 
        try { 
            PrimetimeReference.logger.i(LOG_TAG + "#onResume", 
              "Player restored as activity operations are resumed"); 
            mediaPlayer.restore(); 
        } 
        catch(MediaPlayerException e) { 
            PrimetimeReference.logger.i(LOG_TAG + "#onResume",  
              "Exception occured while restoring mediaPlayer"); 
        } 
    } 
    // Set the fragment paused status to false when app comes in foreground. 
    isActivityPaused = false; 
} 
```
