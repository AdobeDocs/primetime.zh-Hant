---
description: 後期繫結音訊使用PTMediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊串流的視訊。
title: 存取替代音軌
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 存取替代音軌{#access-alternate-audio-tracks}

後期繫結音訊使用PTMediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊串流的視訊。

1. 等待MediaPlayer至少在 `PTMediaPlayerStatusReady` 狀態。
1. 聆聽此事件：

   通知 `PTMediaPlayerItemMediaSelectionOptionsAvailable`：可使用音訊曲目的初始清單。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. 從取得可用的音軌 `PTMediaPlayerItem` 執行個體。

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. （選用）向使用者展示可用的曲目。
1. 將選取的音軌設定在 `PTMediaPlayerItem` 執行個體。
