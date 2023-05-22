---
description: TVSDK使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知播放器客戶端內部AVAsset的availableMediaCharitesWithMediaSelectionOptions的可用性。
title: 曝光字幕
exl-id: 42f15536-39ea-4d83-b501-b05086a0056b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 曝光字幕 {#expose-subtitles}

TVSDK使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知播放器客戶端內部AVAsset的availableMediaCharitesWithMediaSelectionOptions的可用性。

您可以通過 `PTMediaPlayerItem` 屬性 `subtitlesOptions`。

曝光字幕：

1. 將客戶端註冊為 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 通知。

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   當您的客戶端收到此通知時， `PTMediaPlayerItem`。
1. 實施 `onMediaPlayerItemMediaSelectionOptionsAvailable` 方法與以下示例類似：

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   有關備用音頻軌道的資訊，請參見  [備用音頻](../../alternate-audio/ios-3x-alternate-audio.md)。
