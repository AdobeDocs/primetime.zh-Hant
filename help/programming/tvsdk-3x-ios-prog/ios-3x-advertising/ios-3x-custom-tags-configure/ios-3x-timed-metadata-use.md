---
description: 當目前的播放時間符合開始時間時，您可以使用TimedMetadata。
seo-description: 當目前的播放時間符合開始時間時，您可以使用TimedMetadata。
seo-title: 使用計時中繼資料
title: 使用計時中繼資料
uuid: 1531780f-2502-4235-818c-6c0a6bf3d348
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 使用計時中繼資料 {#use-timed-metadata}

當目前的播放時間符合開始時間時，您可以使用TimedMetadata。

若要在播放時使 `PTTimedMetadata` 用這些儲存的物件，請在調度時使用 [Store計時中繼資料物件的儲存字典](../../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-timed-metadata-store.md)。

1. 從此通知擷取並更新目前的播放時間，並尋找所有具有與目 `PTTimedMetadata` 前播放時間相符之開始時間的物件。

   您可以使用這些物件來完成各種動作。

   例如：

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification 
   { 
       CMTimeRange seekableRange = self.player.seekableRange; 
       if (CMTIMERANGE_IS_VALID(seekableRange)) 
       { 
           int currentTime = (int) CMTimeGetSeconds(self.player.currentTime); 
           NSArray *allKeys = timedMetadataCollection ? [timedMetadataCollection allKeys] : [NSArray array]; 
           NSMutableArray *timedMetadatasToDelete = [[[NSMutableArray alloc] init] autorelease]; 
           int count = [allKeys count]; 
   
           for (int i=count - 1; i > -1; i--) 
           { 
              NSNumber *currTimedMetadataTime = allKeys[i]; 
              if ([currTimedMetadataTime integerValue] == currentTime) 
              { 
               /* 
                   Use the timed metadata here and remove it from the collection. 
               */ 
                NSLog (@"IN PLAYBACK TIME %i TO EXECUTE TIMEDMETADATA %@ scheduled at time %f",currentTime,currTimedMetadata.name,CMTimeGetSeconds(currTimedMetadata.time)); 
   
               PTTimedMetadata *currTimedMetadata = [timedMetadataCollection objectForKey:currTimedMetadataTime]; 
               [timedMetadatasToDelete addObject:currTimedMetadataTime]; 
              } 
           } 
   
           for (int i=0; i<[timedMetadatasToDelete count]; i++) 
           { 
               NSNumber *timedMetadataToDelete = timedMetadatasToDelete[i]; 
               [timedMetadataCollection removeObjectForKey:timedMetadataToDelete]; 
           } 
       } 
   }
   ```

1. 定期刷新列 `PTTimedMetadata` 表中的過時實例，以防止記憶體持續增長。