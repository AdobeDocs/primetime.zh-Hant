---
description: TVSDK提供API和示例代碼以處理封鎖期。
title: 實現封鎖處理
exl-id: 9b23674d-76d5-4879-b595-3a6e368c45cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 實現封鎖處理{#implement-blackout-handling}

TVSDK提供API和示例代碼以處理封鎖期。

要實現封鎖處理，包括在封鎖期間提供備用內容：

1. 設定應用以檢測即時流清單中的封鎖標籤。

   ```java
   public void createMediaPlayer { 
       ... 
       String[] blackoutTags = {BLACKOUTTAG}; 
       PSDKConfig.setSubscribedTags(blackoutTags); 
       // For example: PTSDKConfig.setSubscribedTags({"#EXT-OATCLS-SCTE35"}); 
   }
   ```

1. 為前台流和後台流中的定時元資料事件建立事件偵聽器。

   ```java
   private MediaPlayer createMediaPlayer() { 
       mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, _playbackEventListener); 
       mediaPlayer.addEventListener(MediaPlayer.Event.BLACKOUTS, _blackoutsEventListener); 
   }
   ```

1. 為前台流和後台流實現定時元資料事件處理程式。

   前景：

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
             new MediaPlayer.PlaybackEventListener() { 
       ... 
   
       @override 
       public void onTimedMetadata(TimedMetadata timedMetadata) { 
           if (timedMetadata.getName().equal(BLACKOUTTAG) &&  
               !_timedMetadataList.contains(timedMetadata)) { 
                 _timedMetadataList.add(timedMetadata); 
           } 
       } 
       ... 
   } 
   
   private final MediaPlayer.BlackoutsEventListener _blackoutsEventListener =  
     new MediaPlayer.BlackoutsEventListener() { 
       @Override 
       public void onTimedMetadataInBackgroundItem(TimedMetadata timedMetadata) { 
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.TAG) && _mediaPlayer.getPlaybackRange() != null  
               && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               if (!_timedMetadataList.contains(timedMetadata) && isBlackoutMetadata(timedMetadata)) { 
                   _timedMetadataList.add(timedMetadata); 
               } 
           } 
       } 
   
       @Override 
       public void onBackgroundManifestFailed() { 
           ... 
       } 
   }; 
   ```

1. 手柄 `TimedMetadata` 對象 `MediaPlayer` 時間。

   ```java
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   /* handle timedmetadata object list  */ 
                   if (_mediaPlayer != null && _timedMetadataList != null  
                       && _timedMetadataList.size() > 0) { 
                       if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) { 
                           long localTime = _mediaPlayer.getLocalTime(); 
                           handleTimedMetadataList(localTime);      
                       } 
                   } 
               }                        
           }); 
       } 
   };
   ```

1. 建立用於在封鎖期開始和結束時切換內容的方法。

   ```java
   private void handleTimedMetadataList(long currentTime) { 
       for (int i = 0; i < _timedMetadataList.size(); i++) { 
           TimedMetadata timedMetadata = _timedMetadataList.get(i); 
           long diff = localTime - timedMetadata.getTime(); 
           if (!_timedMetadataDispatchedList.contains(timedMetadata) 
               && diff >= 0 
               && diff <= PLAYBACK_CLOCK_INTERVAL 
               && _mediaPlayer.shouldTriggerSubscribedTagEvent()) { 
                   // switch to blackout content 
               if (!_inBlackout && isBlackoutStartTimedMetadata(timedMetadata)) { 
                   MediaResource blackoutMediaResource = createBlackoutMediaResource(timedMetadata); 
   
                   //1. register current item as background item 
                   _mediaPlayer.registerCurrentItemAsBackgroundItem(); 
   
                   //2. replace current item with blackout item 
                   _mediaPlayer.replaceCurrentItem(blackoutMediaResource); 
   
                   //3. update qos metrics 
                   _mediaQosProvider.updateMetrics(_mediaPlayer); 
   
                   //4. maintain state 
                   _inBlackout = true; 
                   resetTimedMetada(); 
   
                   break; 
               } 
               // switch back to main content 
               else if (_inBlackout && isBlackoutEndTimedMetadata(timedMetadata)) { 
                   //1. register current item as background item 
                   _mediaPlayer.unregisterCurrentBackgroundItem(); 
   
                   //2. replace current item with blackout item 
                   _mediaPlayer.replaceCurrentItem(_oldMediaResource); 
   
                   //3. update qos metrics 
                   _mediaQosProvider.updateMetrics(_mediaPlayer); 
   
                   //4. maintain state 
                   _inBlackout = false; 
                   resetTimedMetada(); 
   
                   break; 
               } 
           } 
       } 
   }
   ```

1. 如果封鎖範圍在播放流的DVR中，則更新不可查找的範圍。

   ```java
   // prepare and update blackout nonSeekable ranges 
   
   List<TimeRange> blackoutRanges = prepareBlackoutRanges(_timedMetadataList); 
   if (blackoutRanges != null && blackoutRanges.size() > 0) { 
       int size = blackoutRanges.size(); 
       TimeRange[] blackoutRangesArray = blackoutRanges.toArray(new TimeRange[size]); 
       BlackoutMetadata blackoutMetadata = new BlackoutMetadata(blackoutRangesArray); 
       updateBlackoutMetadata(blackoutMetadata); 
   } 
   
   // function to update blackout metadata 
   private void updateBlackoutMetadata(BlackoutMetadata blackoutMetadata) { 
       MediaPlayerItem currentItem = _mediaPlayer.getCurrentItem(); 
       if (currentItem != null) { 
           Metadata metadata = currentItem.getResource().getMetadata(); 
           if (metadata != null) { 
               MetadataNode metadataNode = ((MetadataNode) metadata); 
               metadataNode.setNode(DefaultMetadataKeys.BLACKOUT_METADATA_KEY.getValue(),  
                                    blackoutMetadata); 
   
               for (int i = 0; i < blackoutMetadata.getNonSeekableRanges().length; i++) { 
                   TimeRange timeRange = blackoutMetadata.getNonSeekableRanges()[i]; 
               } 
           } 
       } 
   }
   ```

   >[!NOTE]
   >
   >目前，對於多位率即時流，有時可調位率(ABR)配置檔案會失去同步。 這會導致重複 `timedMetadata` 同一訂閱標籤的對象。 為避免不正確的不可瀏覽計算，強烈建議在計算後檢查重疊的不可瀏覽範圍，如下例所示：

   ```java
   List<TimeRange> rangesToRemove = new ArrayList<TimeRange>(); 
   
   for (int i = 0; i < nonSeekableRanges.size() - 1; i++) { 
       TimeRange range1 = nonSeekableRanges.get(i); 
       TimeRange range2 = nonSeekableRanges.get(i + 1); 
       if (range1.contains(range2.getBegin()) && !rangesToRemove.contains(range2)) { 
          rangesToRemove.add(range2); 
       } else if (range2.contains(range1.getBegin()) && !rangesToRemove.contains(range1)) { 
          rangesToRemove.add(range1); 
      } 
   } 
   
   if (nonSeekableRanges.size() > 0 && rangesToRemove.size() > 0) { 
       nonSeekableRanges.removeAll(rangesToRemove); 
       for (int i = 0; i < rangesToRemove.size(); i++) { 
           TimeRange range = rangesToRemove.get(i); 
       } 
   } 
   
   if (nonSeekableRanges.size() > 0 && rangesToRemove.size() > 0) { 
       nonSeekableRanges.removeAll(rangesToRemove); 
   }
   ```
