---
description: 當目前的播放時間符合開始時間時，您可以使用TimedMetadata。
title: 使用定時中繼資料
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 使用定時中繼資料 {#use-timed-metadata}

當目前的播放時間符合開始時間時，您可以使用TimedMetadata。

若要使用這些已儲存的 `TimedMetadata` 物件在播放期間，使用已儲存的 `ArrayList` 從 [在傳送時儲存定時中繼資料物件](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. 執行計時器並重複查詢目前的播放時間。
1. 尋找所有 `TimedMetadata` 開始時間符合目前播放時間的物件。

   您可以使用這些物件完成各種動作。

   >[!IMPORTANT]
   >
   >檢查目前的播放時間是否符合任何設定時 `TimedMetadata` 物件，包括 `shouldTriggerSubscribedTagEvent` 作為條件。

   時間軸可能會因各種廣告行為而變更。 例如，一個或多個廣告插播可能會從他們在時間軸上的原始位置移動，但是 `shouldTriggerSubscribedTagEvent` 確保 `TimeMetadata` 物件的開始時間符合目前的播放時間。

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

1. 定期排清陳舊 `TimedMetadata` 清單中的例項，以防止記憶體持續成長。
