---
description: TVSDK會使用PTMediaPlayerMediaSelectionOptionsAvailableNotification，通知您的播放器用戶端有關內部AVAsset的availableMediaCherationsWithMediaSelectionOptions的可用性。
seo-description: TVSDK會使用PTMediaPlayerMediaSelectionOptionsAvailableNotification，通知您的播放器用戶端有關內部AVAsset的availableMediaCherationsWithMediaSelectionOptions的可用性。
seo-title: 顯示字幕
title: 顯示字幕
uuid: 1cd8761f-6e6f-4017-9852-fa61f36197c5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 顯示字幕{#expose-subtitles}

TVSDK會使用PTMediaPlayerMediaSelectionOptionsAvailableNotification，通知您的播放器用戶端有關內部AVAsset的availableMediaCherationsWithMediaSelectionOptions的可用性。

您可以透過`PTMediaPlayerItem`屬性的`subtitlesOptions`存取可用的字幕。

要公開字幕：

1. 將客戶機註冊為`PTMediaPlayerMediaSelectionOptionsAvailableNotification`通知的監聽器。

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   當您的客戶收到此通知時，`PTMediaPlayerItem`中的字幕就緒。
1. 實作類似下列範例的`onMediaPlayerItemMediaSelectionOptionsAvailable`方法：

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   如需替代音軌的詳細資訊，請參閱[替代音訊](../../alternate-audio/ios-3x-alternate-audio.md)。