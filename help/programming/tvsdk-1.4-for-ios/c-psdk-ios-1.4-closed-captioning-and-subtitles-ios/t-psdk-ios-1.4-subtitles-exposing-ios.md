---
description: TVSDK會使用PTMmediaPlayerMediaSelectionOptionsAvailableNotification通知，通知播放器使用者端內部AVAset的availableMediaCharacticesWithMediaSelectionOptions可用性。
title: 公開字幕
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 公開字幕 {#expose-subtitles}

TVSDK會使用PTMmediaPlayerMediaSelectionOptionsAvailableNotification通知，通知播放器使用者端內部AVAset的availableMediaCharacticesWithMediaSelectionOptions可用性。

您可以透過 `PTMediaPlayerItem` 屬性的 `subtitlesOptions`.

若要公開字幕：

1. 將從屬端註冊為監聽器 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 通知。

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   當您的使用者端收到此通知時，字幕已可在 `PTMediaPlayerItem`.
1. 實作 `onMediaPlayerItemMediaSelectionOptionsAvailable` 方法與下列範例類似：

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   如需其他音訊曲目的相關資訊，請參閱  [替代音訊](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).
