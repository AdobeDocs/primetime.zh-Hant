---
description: 後期綁定音頻使用PTMediaPlayer播放在M3U8 HLS播放清單中指定的可包含多個備用音頻流的視頻。
title: 訪問備用音頻軌道
exl-id: f3ab9573-c189-4132-820d-0ce98ee170d1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 訪問備用音頻軌道{#access-alternate-audio-tracks}

後期綁定音頻使用PTMediaPlayer播放在M3U8 HLS播放清單中指定的可包含多個備用音頻流的視頻。

1. 等待MediaPlayer至少位於 `PTMediaPlayerStatusReady` 狀態。
1. 收聽此事件：

   通知 `PTMediaPlayerItemMediaSelectionOptionsAvailable`:音頻軌道的初始清單可用。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. 從 `PTMediaPlayerItem` 實例。

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. （可選）向用戶顯示可用的軌道。
1. 在 `PTMediaPlayerItem` 實例。
