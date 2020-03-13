---
description: 當使用者按一下廣告時，您的應用程式應暫停播放主要視訊內容。
seo-description: 當使用者按一下廣告時，您的應用程式應暫停播放主要視訊內容。
seo-title: 暫停並繼續播放
title: 暫停並繼續播放
uuid: 229e2499-e30e-458c-bd6d-d035588c21cf
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 暫停並繼續播放 {#pause-and-resume-playback}

當使用者按一下廣告時，您的應用程式應暫停播放主要視訊內容。

1. 覆寫和 `onPause` 從 `onResume` Android活動。

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       requestAudioFocus(); 
       if (_lastKnownStatus == MediaPlayerStatus.PAUSED) { 
           _mediaPlayer.play(); 
       } 
   } 
   ... 
   
   @Override 
   public void onPause() { 
       super.onPause(); 
       if (_mediaPlayer != null) { 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING || 
             _mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) { 
               _savedPlayerStatus = _mediaPlayer.getStatus(); 
               _lastKnownTime = _mediaPlayer.getCurrentTime(); 
           } 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
               _mediaPlayer.pause(); 
               _lastKnownStatus = MediaPlayerStatus.PAUSED; 
           } 
       } 
   } 
   abandonAudioFocus(); 
   ```

