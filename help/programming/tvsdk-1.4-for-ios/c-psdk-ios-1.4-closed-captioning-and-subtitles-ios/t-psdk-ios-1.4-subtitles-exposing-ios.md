---
description: TVSDK會使用PTMediaPlayerMediaSelectionOptionsAvailableNotification，通知您的播放器用戶端有關內部AVAsset的availableMediaCherationsWithMediaSelectionOptions的可用性。
seo-description: TVSDK會使用PTMediaPlayerMediaSelectionOptionsAvailableNotification，通知您的播放器用戶端有關內部AVAsset的availableMediaCherationsWithMediaSelectionOptions的可用性。
seo-title: 顯示字幕
title: 顯示字幕
uuid: 657ab9c7-b205-4d13-81a7-51bc8e7d5ee2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 顯示字幕 {#expose-subtitles}

TVSDK會使用PTMediaPlayerMediaSelectionOptionsAvailableNotification，通知您的播放器用戶端有關內部AVAsset的availableMediaCherationsWithMediaSelectionOptions的可用性。

您可以透過屬性的存取可 `PTMediaPlayerItem` 用字幕 `subtitlesOptions`。

要公開字幕：

1. 將客戶機註冊為通知的偵聽 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 器。

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   當您的客戶收到此通知時，字幕已在中準備好 `PTMediaPlayerItem`。
1. 實作類 `onMediaPlayerItemMediaSelectionOptionsAvailable` 似下列範例的方法：

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   如需替代音軌的詳細資訊，請參閱 [替代音訊](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md)。