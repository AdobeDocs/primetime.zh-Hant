---
description: 當當前播放時間與開始時間匹配時，可以使用TimedMetadata。
title: 使用定時元資料
exl-id: 7f87cd14-121a-4543-ab0a-a03d829d040b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 使用定時元資料 {#use-timed-metadata}

當當前播放時間與開始時間匹配時，可以使用TimedMetadata。

使用這些保存的 `TimedMetadata` 回放期間的對象，使用已保存的 `ArrayList` 從 [在調度時儲存定時元資料對象](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md)。

1. 運行計時器並重複查詢當前播放時間。
1. 查找所有 `TimedMetadata` 對象的起始時間與當前回放時間匹配。

   可以使用這些對象完成各種操作。

   >[!IMPORTANT]
   >
   >檢查當前回放時間是否與任何 `TimedMetadata` 對象，包括 `shouldTriggerSubscribedTagEvent` 作為條件。

   時間線可能會因各種廣告行為而改變。 例如，一個或多個廣告分段可能從它們在時間軸上的原始位置移動，但 `shouldTriggerSubscribedTagEvent` 確保 `TimeMetadata` 對象的開始時間與當前回放時間匹配。

   例如：

   ```java
    _playbackClockEventListener = new Clock.ClockEventListener() {
       @Override
       public void onTick(String name) {
           getActivity().runOnUiThread(new Runnable() {
               @Override
               public void run() {
                   /* handle timedmetadata object list  */ 
                   if (_mediaPlayer != null && _timedMetadataList != null && _timedMetadataList.size() > 0) {
                       if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) {
                           long localTime = _mediaPlayer.getLocalTime();
                           Iterator<TimedMetadata> iterator = _timedMetadataList.iterator(); 
                           while (iterator.hasNext()) {
                               TimedMetadata timedMetadata = iterator.next();
                               long diff = localTime - timedMetadata.getTime();
                               if (diff >= 0 &&
                                   diff <= PLAYBACK_CLOCK_INTERVAL &&
                                   _mediaPlayer.shouldTriggerSubscribedTagEvent()) {
                                   // use timed metadata object
                               }
                           }
                       }
                   }
               }
           });
       }
   };
   _playbackClock.addClockEventListener(_playbackClockEventListener);
   ```

1. 定期刷新陳舊 `TimedMetadata` 從清單中實例，以防止記憶體持續增長。
