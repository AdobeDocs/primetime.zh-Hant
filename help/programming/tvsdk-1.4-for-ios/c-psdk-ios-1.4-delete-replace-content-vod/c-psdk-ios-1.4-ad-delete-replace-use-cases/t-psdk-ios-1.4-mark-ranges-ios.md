---
description: 'null'
seo-description: 'null'
seo-title: 標籤範圍
title: 標籤範圍
uuid: 994a8f07-0951-47ec-b21a-d74c9eeefd74
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 標籤範圍{#mark-ranges}

若要實作內 `PTTimeRangeCollection` 容範圍並標示為廣告：
1. 準備 `PTTimeRangeCollection`。
1. 將類型設定為 `PTTimeRangeCollection``PTTimeRangeCollectionTypeMarkRanges`。

   此步驟會通知TVSDK自訂範圍必須視為廣告。

   ```
   #define PSDK_TIMESCALE 100000 
   
   NSArray *ranges =  @[ 
     [PTReplacementRange  
       replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
         (0, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))], 
     [PTReplacementRange  
       replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
         (120, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))] 
   ]; 
   
   PTTimeRangeCollection *timeRangeCollection =  
     [[PTTimeRangeCollection alloc] initWithRanges:ranges  
       type:PTTimeRangeCollectionTypeMarkRanges];
   ```

1. 建立 `PTAdMetadata` 並設定 `PTTimeRangeCollection`。

   ```
   // Create the PTPlayerItem metadata 
   PTMetadata *metadata = [[PTMetadata alloc] init]; 
   
   // Create the Ad metadata 
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init]; 
   adMetadata.timeRangeCollection = timerangeCollection; 
   
   //Set Ad metadata 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
   //Create PTMediaPlayerItem 
   PTMediaPlayerItem *playerItem = [[[PTMediaPlayerItem alloc] initWithUrl:mediaUrl 
                                                                   mediaId:mediaId 
                                                                  metadata:metadata];
   ```

1. 建立播放器並開始播放。

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
   
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
   
   //Start playback 
   [player play];
   ```

## 取代範圍{#replace-ranges}

要將內容范 `PTTimeRangeCollection` 圍實作並刪除為廣告：
1. 準備 `PTTimeRangeCollection`。
1. 將類型設定為 `PTTimeRangeCollection``PTTimeRangeCollectionTypeReplaceRanges`。

   此步驟會通知TVSDK必須以替代內容（廣告）來取代提供的範圍。

   ```
   #define PSDK_TIMESCALE 100000 
   
   NSArray *ranges =  @[ 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (0, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))  
       replacementDuration:CMTimeMakeWithSeconds(30, AD_TIMESCALE)], 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (120, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))  
       replacementDuration:CMTimeMakeWithSeconds(30, AD_TIMESCALE)] 
                       ]; 
   
   PTTimeRangeCollection *timeRangeCollection =  
     [[PTTimeRangeCollection alloc] initWithRanges:ranges  
                                              type:PTTimeRangeCollectionTypeReplaceRanges];
   ```

   >[!TIP]
   >
   >此引數 `replacementDuration` 為可選。 如果未定義，則 `AdServer` 會決定廣告分段的持續時間。

1. 建立 `PTAdMetadata` 並設定 `PTTimeRangeCollection`。

   ```
   //Create the PTPlayerItem metadata 
   PTMetadata *metadata = [[PTMetadata alloc] init]; 
   
   //Create the Ad metadata 
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init]; 
   adMetadata.timeRangeCollection = timerangeCollection; 
   adMetadata.zoneId = adZoneId; 
   adMetadata.domain = adDomain; 
   adMetadata.signalingMode = PTAdSignalingModeCustomRanges; 
   
   //Set Ad metadata 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
   //Create PTMediaPlayerItem 
   PTMediaPlayerItem *playerItem = [[[PTMediaPlayerItem alloc] initWithUrl:mediaUrl 
                                                                   mediaId:mediaId 
                                                                  metadata:metadata];
   ```

   >[!TIP]
   >
   >雖然設 `signalingMode` 置為 `PTAdSignalingModeCustomRanges`，但在設定類型時會自動設定此廣 `PTTimeRangeCollection` 告信令模式 `PTTimeRangeCollectionTypeReplace`。

1. 建立播放器並開始播放。

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
   
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
   
   //Start playback 
   [player play];
   ```

## 刪除範圍 {#delete-ranges}

要將內容范 `PTTimeRangeCollection` 圍實作並刪除為廣告：
1. 準備 `PTTimeRangeCollection`。
1. 將類型設為 `PTTimeRangeCollection` , `PTTimeRangeCollectionTypeDeleteRanges`會通知TVSDK必須刪除提供的範圍。

   ```
   #define PSDK_TIMESCALE 100000 
   
   NSArray *ranges =  @[ 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (0, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))], 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (120, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))] 
   ]; 
   
   PTTimeRangeCollection *timeRangeCollection =  
     [[PTTimeRangeCollection alloc] initWithRanges:ranges  
                                              type:PTTimeRangeCollectionTypeDeleteRanges];
   ```

1. 建立 `PTAdMetadata` 並設定 `PTTimeRangeCollection`。

   ```
   //Create the PTPlayerItem metadata 
   PTMetadata *metadata = [[PTMetadata alloc] init]; 
   
   //Create the Ad metadata 
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init]; 
   adMetadata.timeRangeCollection = timerangeCollection; 
   adMetadata.zoneId = adZoneId; 
   adMetadata.domain = adDomain; 
   adMetadata.signalingMode = PTAdSignalingModeServerMap; 
   
   //Set Ad metadata 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
   //Create PTMediaPlayerItem 
   PTMediaPlayerItem *playerItem = [[[PTMediaPlayerItem alloc] initWithUrl:mediaUrl 
                                                                   mediaId:mediaId 
                                                                  metadata:metadata];
   ```

   >[!TIP]
   >
   >廣告插入會在根據和目前刪除自訂範圍 `PTAdMetadata` 後發生 `PTAdSignalingMode`。

1. 建立播放器並開始播放。

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
   
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
   
   //Start playback 
   [player play];
   ```
