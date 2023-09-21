---
description: TVSDK支援在隨選視訊(VOD)和即時資料流中，搜尋資料流為滑動視窗播放清單的特定位置（時間）。
title: 顯示具有目前播放位置的搜尋拖曳列
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 顯示具有目前播放位置的搜尋拖曳列 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支援在隨選視訊(VOD)和即時資料流中，搜尋資料流為滑動視窗播放清單的特定位置（時間）。

>[!IMPORTANT]
>
>只有DVR才允許在即時資料流中進行搜尋。

1. 設定搜尋的回呼。

       搜尋為非同步，因此TVSDK會傳送下列搜尋相關事件：
   
   * `QOSEventListener.onSeekStart`  — 搜尋開始。
   * `QOSEventListener.onSeekComplete`  — 搜尋成功。
   * `QOSEventListener.onOperationFailed`  — 搜尋失敗。

1. 等候播放器處於有效的搜尋狀態。

   有效的狀態包括「已準備」、「完成」、「已暫停」和「正在播放」。

1. 使用原生搜尋列來設定 `OnSeekBarChangeListener` 以檢視使用者何時拖曳。
1. 聆聽 `QOSEventListener.onOperationFailed` 並採取適當的動作。

   此事件會通過適當的警告。 您的應用程式會決定如何繼續，例如，再次嘗試搜尋或從上一個位置繼續播放。

1. 等待TVSDK呼叫 `QOSEventListener.onSeekComplete` 回撥。
1. 使用回呼的position引數擷取最後調整的播放位置。

   這很重要，因為搜尋之後的實際開始位置可能與要求的位置不同。 如果搜尋或其他重新定位在廣告插播中途結束，或略過廣告插播，可能會影響播放行為。

1. 顯示搜尋拖曳列時使用位置資訊。

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**搜尋範例**

在此範例中，使用者拖曳搜尋列以搜尋至所要的位置。

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
