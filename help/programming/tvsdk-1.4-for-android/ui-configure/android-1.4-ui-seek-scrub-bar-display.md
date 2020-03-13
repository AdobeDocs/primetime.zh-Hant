---
description: TVSDK支援搜尋特定位置（時間），其中串流為隨選視訊(VOD)和即時串流中的滑動視窗播放清單。
seo-description: TVSDK支援搜尋特定位置（時間），其中串流為隨選視訊(VOD)和即時串流中的滑動視窗播放清單。
seo-title: 顯示具有當前回放位置的查找拖曳條
title: 顯示具有當前回放位置的查找拖曳條
uuid: a9f4dd6c-78cf-455c-8c31-b2f7b740d84a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 顯示具有當前回放位置的查找拖曳條 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支援搜尋特定位置（時間），其中串流為隨選視訊(VOD)和即時串流中的滑動視窗播放清單。

>[!IMPORTANT]
>
>在即時串流中搜尋僅允許DVR使用。

1. 設定搜索回呼。

       搜尋是非同步的，因此TVSDK會調派下列搜尋相關事件：
   
   * `QOSEventListener.onSeekStart` -尋求開始。
   * `QOSEventListener.onSeekComplete` -尋求成功。
   * `QOSEventListener.onOperationFailed` -搜索失敗。

1. 等待玩家處於有效狀態進行搜尋。

   有效狀態包括準備、完成、暫停和播放。

1. 使用原生SeekBar來設 `OnSeekBarChangeListener` 定查看使用者拖曳的時間。
1. 傾聽並 `QOSEventListener.onOperationFailed` 採取適當行動。

   此事件會傳遞適當的警告。 例如，您的應用程式會決定如何繼續，方法是再次嘗試搜尋或從上一個位置繼續播放。

1. 等待TVSDK呼叫回 `QOSEventListener.onSeekComplete` 呼。
1. 使用回呼的位置參數擷取最終調整的播放位置。

   這很重要，因為搜尋後的實際開始位置可能與請求的位置不同。 如果搜尋或其他重新定位在廣告插播的中間結束或跳過廣告插播，則播放行為可能會受到影響。

1. 在顯示搜尋拖曳列時使用位置資訊。

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**搜尋範例**

在此範例中，使用者將搜尋列拖曳至所要的位置。

```java
// Use the native SeekBar to set OnSeekBarChangeListener to  
//see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) {  
            // Update the seek bar thumb, with the position provided by the user. 
            setPosition(progress); 
        } 
    } 
 
    @Override 
    public void onStartTrackingTouch(SeekBar seekBar) { 
        isSeeking = true; 
    } 
 
    @Override 
    public void onStopTrackingTouch(SeekBar seekBar) { 
        isSeeking = false; 
        // Retrieve the playback range. 
        TimeRange playbackRange = mediaPlayer.getPlaybackRange(); 
        // Make sure to seek inside the playback range. 
        long seekPosition = Math.min(Math.round(seekBar.getProgress()),  
                                     playbackRange.getDuration()); 
        // Perform seek. 
        seek(playbackRange.getBegin() + seekPosition); 
    } 
}; 
```

