---
description: 當目前的播放時間符合開始時間時，您可以使用TimedMetadata。
seo-description: 當目前的播放時間符合開始時間時，您可以使用TimedMetadata。
seo-title: 使用計時中繼資料
title: 使用計時中繼資料
uuid: 98bb8c08-2794-42d6-b5c3-b1047ac804fe
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 使用計時中繼資料 {#use-timed-metadata}

當目前的播放時間符合開始時間時，您可以使用TimedMetadata。

若要在播放時使 `TimedMetadata` 用這些儲存的物件，請在調度時 `ArrayList` 使 [用從Store計時中繼資料物件儲存的物件](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md)。

1. 執行計時器並重複查詢目前的播放時間。
1. 尋找所有具有 `TimedMetadata` 與目前播放時間相符之開始時間的物件。

   您可以使用這些物件來完成各種動作。

[!IMPORTANT]
檢查當前播放時間是否與任何對象匹 `TimedMetadata` 配時，請將 `shouldTriggerSubscribedTagEvent` 其作為條件包含。

時間軸可能會因各種廣告行為而改變。 例如，一個或多個廣告插播可能會從時間軸上的原始位置移 `shouldTriggerSubscribedTagEvent` 動，但 `TimeMetadata` 會確保物件的開始時間符合目前播放時間。

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

1. 定期刷新列 `TimedMetadata` 表中的過時實例，以防止記憶體持續增長。