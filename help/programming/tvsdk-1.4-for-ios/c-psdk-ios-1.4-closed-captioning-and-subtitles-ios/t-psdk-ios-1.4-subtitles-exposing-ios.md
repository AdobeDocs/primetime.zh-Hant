---
description: TVSDK會使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知，通知播放器使用者端內部AVAset的availableMediaCharacticesWithMediaSelectionOptions的可用性。
title: 公開字幕
exl-id: dc726a5b-2eab-4ebd-8773-7396bf818205
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 公開字幕 {#expose-subtitles}

TVSDK會使用PTMediaPlayerMediaSelectionOptionsAvailableNotification通知，通知播放器使用者端內部AVAset的availableMediaCharacticesWithMediaSelectionOptions的可用性。

您可以透過以下方式存取可用的字幕： `PTMediaPlayerItem` 屬性的 `subtitlesOptions`.

若要公開字幕：

1. 將從屬端註冊為監聽器 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 通知。

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   當您的客戶收到此通知時，字幕已可在 `PTMediaPlayerItem`.
1. 實作 `onMediaPlayerItemMediaSelectionOptionsAvailable` 方法與下列範例類似：

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   如需替代音軌的相關資訊，請參閱  [替代音訊](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).
