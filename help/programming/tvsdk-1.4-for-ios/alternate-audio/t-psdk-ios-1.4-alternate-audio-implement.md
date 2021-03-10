---
description: 延遲系結音訊使用PTMediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
title: 存取替代音軌
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# 存取替代音軌{#access-alternate-audio-tracks}

延遲系結音訊使用PTMediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。

1. 等待MediaPlayer至少處於`PTMediaPlayerStatusReady`狀態。
1. 聽取此事件：

   通知`PTMediaPlayerItemMediaSelectionOptionsAvailable`:音軌的初始清單可供使用。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. 從`PTMediaPlayerItem`實例獲取可用的音軌。

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. （選擇性）向使用者呈現可用的追蹤。
1. 在`PTMediaPlayerItem`實例上設定選定的音軌。
