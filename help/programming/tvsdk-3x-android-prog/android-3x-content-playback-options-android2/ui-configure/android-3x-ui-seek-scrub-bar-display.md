---
description: TVSDK支援在隨選影片(VOD)和即時資料流中，搜尋資料流為滑動視窗播放清單的特定位置（時間）。
title: 顯示具有目前播放位置的搜尋拖曳列
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 顯示具有目前播放位置的搜尋拖曳列 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支援在隨選影片(VOD)和即時資料流中，搜尋資料流為滑動視窗播放清單的特定位置（時間）。

>[!TIP]
>
>只有DVR才允許在即時資料流中進行搜尋。

1. 設定搜尋的回呼。

   搜尋為非同步，因此TVSDK會傳送下列搜尋相關事件：

   * `MediaPlayerEvent.SEEK_BEGIN`，搜尋的開始位置。
   * `MediaPlayerEvent.SEEK_END`，搜尋成功的位置。
   * `MediaPlayerEvent.OPERATION_FAILED`，搜尋已失敗。

1. 等候播放器處於有效的搜尋狀態。

   有效狀態為「已準備」、「完成」、「已暫停」和「正在播放」。
1. 使用原生 `SeekBar` 要設定 `OnSeekBarChangeListener`，會決定使用者何時拖曳。
1. 將請求的搜尋位置（毫秒）傳遞至 `MediaPlayer.seek` 方法。

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   您只能搜尋資產的可搜尋期間。 若為隨選影片，即從0到資產的持續時間。

   >[!TIP]
   >
   >此步驟會將播放磁頭移動到串流中的新位置，但最終計算位置可能與指定的搜尋位置不同。

1. 聆聽 `MediaPlayerEvent.OPERATION_FAILED` 並採取適當的動作。

   此事件會通過適當的警告。 您的應用程式會決定如何繼續，選項包括再次嘗試搜尋或從上一個位置繼續播放。

1. 等待TVSDK呼叫 `MediaPlayerEvent.SEEK_END` 回撥。
1. 使用回呼的position引數擷取最後調整的播放位置。

   這很重要，因為搜尋之後的實際開始位置可能與要求的位置不同。 如果搜尋或其他重新定位作業在廣告插播中途結束，或略過廣告插播，規則（包括播放行為）可能會受到影響。

1. 顯示搜尋拖曳列時使用位置資訊。

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**搜尋範例**

在此範例中，使用者拖曳搜尋列以搜尋至所要的位置。

```java
//Use the native SeekBar to set an OnSeekBarChangeListener to 
// see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) { 
            // Update the seek bar thumb with the position provided by the user. 
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
