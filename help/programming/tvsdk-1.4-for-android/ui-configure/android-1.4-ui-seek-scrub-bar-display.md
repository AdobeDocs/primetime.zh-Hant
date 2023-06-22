---
description: TVSDK支援搜尋串流為滑動視窗播放清單的特定位置（時間），包括隨選視訊(VOD)和即時串流中。
title: 顯示搜尋拖曳列與目前播放位置
exl-id: 8076521b-579d-491f-97de-c7b57daa9b2e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 顯示搜尋拖曳列與目前播放位置 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支援搜尋串流為滑動視窗播放清單的特定位置（時間），包括隨選視訊(VOD)和即時串流中。

>[!IMPORTANT]
>
>只有DVR才允許搜尋即時資料流。

1. 設定搜尋的回呼。

       搜尋為非同步，因此TVSDK會傳送以下搜尋相關事件：
   
   * `QOSEventListener.onSeekStart`  — 搜尋開始。
   * `QOSEventListener.onSeekComplete`  — 搜尋成功。
   * `QOSEventListener.onOperationFailed`  — 搜尋失敗。

1. 等候播放器處於有效的搜尋狀態。

   有效狀態為「已準備」、「完成」、「已暫停」和「正在播放」。

1. 使用原始搜尋列來設定 `OnSeekBarChangeListener` 以檢視使用者何時拖曳。
1. 聆聽 `QOSEventListener.onOperationFailed` 並採取適當的動作。

   此事件會傳遞適當的警告。 您的應用程式會決定如何繼續，例如，再次嘗試搜尋或從上一個位置繼續播放。

1. 等待TVSDK呼叫 `QOSEventListener.onSeekComplete` callback。
1. 使用回呼的位置引數來擷取最終調整後的播放位置。

   這很重要，因為搜尋後的實際開始位置可能與要求的位置不同。 如果搜尋或其他重新定位在廣告插播中途結束，或略過廣告插播，播放行為可能會受到影響。

1. 顯示搜尋清除列時，請使用位置資訊。

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**搜尋範例**

在此範例中，使用者會清除搜尋列，以搜尋至所需的位置。

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
