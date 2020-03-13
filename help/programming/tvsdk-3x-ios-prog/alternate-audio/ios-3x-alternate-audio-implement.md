---
description: 延遲系結音訊使用PTMediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
seo-description: 延遲系結音訊使用PTMediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
seo-title: 存取替代音軌
title: 存取替代音軌
uuid: 2915a74f-5ec3-457e-890d-5c79be39f37a
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 存取替代音軌 {#access-alternate-audio-tracks}

延遲系結音訊使用PTMediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。

1. 等待MediaPlayer至少處於狀 `PTMediaPlayerStatusReady` 態。
1. 聽取此事件：

   通知 `PTMediaPlayerItemMediaSelectionOptionsAvailable`:音軌的初始清單可供使用。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. 從例項取得可用的音軌 `PTMediaPlayerItem` 。

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. （選擇性）向使用者呈現可用的追蹤。
1. 在例項上設定選取的音軌 `PTMediaPlayerItem` 。
