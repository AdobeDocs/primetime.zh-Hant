---
description: TVSDK支援在視頻點播(VOD)和即時流中尋找特定位置（時間），其中流是滑動窗口播放清單。
title: 顯示具有當前回放位置的查找擦除欄
exl-id: fb1a87ec-30ab-4dbe-9744-720eac523542
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 顯示具有當前回放位置的查找擦除欄 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支援在視頻點播(VOD)和即時流中尋找特定位置（時間），其中流是滑動窗口播放清單。

>[!TIP]
>
>只允許DVR在即時流中查找。

1. 設定尋找回調。

       搜索是非同步的，因此TVSDK會調度以下與搜索相關的事件：
   
   * `MediaPlayerEvent.SEEK_BEGIN`，尋道開始的位置。
   * `MediaPlayerEvent.SEEK_END`，其中查找成功。
   * `MediaPlayerEvent.OPERATION_FAILED`，查找失敗的位置。

1. 等待玩家處於有效狀態以進行查找。

   有效狀態為「準備」、「完成」、「暫停」和「播放」。
1. 使用本機 `SeekBar` 設定 `OnSeekBarChangeListener`，確定用戶正在清理的時間。
1. 將請求的查找位置（毫秒）傳遞到 `MediaPlayer.seek` 的雙曲餘切值。

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   您只能在資產的可尋的持續時間內查找。 對於視頻點播，從0到資產的持續時間。

   >[!TIP]
   >
   >此步驟將播放頭移動到流中的新位置，但最終計算位置可能與指定的查找位置不同。

1. 聽 `MediaPlayerEvent.OPERATION_FAILED` 採取適當行動。

   此事件會傳遞相應的警告。 您的應用程式確定如何繼續，這些選項包括再次嘗試查找或從上一位置繼續回放。

1. 等待TVSDK調用 `MediaPlayerEvent.SEEK_END` 回叫。
1. 使用回調的位置參數檢索最終調整的播放位置。

   這一點很重要，因為在搜索之後的實際開始位置可能與請求的位置不同。 如果搜索或其他重新定位結束於廣告分段的中間或跳過廣告分段，則規則（包括回放行為）可能會受到影響。

1. 在顯示查找清理欄時使用位置資訊。

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**尋找示例**

在本例中，用戶將搜索條掃描到所需位置。

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
