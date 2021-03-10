---
description: 當目前的播放時間符合開始時間時，您可以使用TimedMetadata。
title: 使用計時中繼資料
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 1%

---


# 使用計時中繼資料{#use-timed-metadata}

當目前的播放時間符合開始時間時，您可以使用TimedMetadata。

若要在播放期間使用這些保存的`TimedMetadata`對象，請使用[儲存調度的計時元資料對象中保存的`ArrayList`。](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md)

1. 執行計時器並重複查詢目前的播放時間。
1. 尋找所有`TimedMetadata`物件，其開始時間與目前播放時間相符。

   您可以使用這些物件來完成各種動作。

   >[!IMPORTANT]
   >
   >檢查當前播放時間是否與任何`TimedMetadata`對象匹配時，請將`shouldTriggerSubscribedTagEvent`作為條件。

   時間軸可能會因各種廣告行為而改變。 例如，一個或多個廣告插播可能會從它們在時間軸上的原始位置移動，但`shouldTriggerSubscribedTagEvent`可確保`TimeMetadata`物件的開始時間符合目前的播放時間。

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

1. 定期刷新清單中的過時`TimedMetadata`實例，以防止記憶體持續增長。