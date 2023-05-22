---
description: TVSDK支援在視頻點播(VOD)和即時流中尋找特定位置（時間），其中流是滑動窗口播放清單。
title: 顯示具有當前回放位置的查找擦除欄
exl-id: 8076521b-579d-491f-97de-c7b57daa9b2e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 顯示具有當前回放位置的查找擦除欄 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支援在視頻點播(VOD)和即時流中尋找特定位置（時間），其中流是滑動窗口播放清單。

>[!IMPORTANT]
>
>只允許DVR在即時流中查找。

1. 設定尋找回調。

       搜索是非同步的，因此TVSDK會調度以下與搜索相關的事件：
   
   * `QOSEventListener.onSeekStart`  — 尋找開始。
   * `QOSEventListener.onSeekComplete`  — 尋求成功。
   * `QOSEventListener.onOperationFailed`  — 查找失敗。

1. 等待玩家處於有效狀態以進行查找。

   有效狀態包括PREPARED、COMPLETE、PAUSED和PLAYING。

1. 使用本機SeekBar設定 `OnSeekBarChangeListener` 查看用戶正在清理的時間。
1. 聽 `QOSEventListener.onOperationFailed` 採取適當行動。

   此事件會傳遞相應的警告。 例如，您的應用程式通過再次嘗試查找或從上一位置繼續回放來確定如何繼續。

1. 等待TVSDK調用 `QOSEventListener.onSeekComplete` 回叫。
1. 使用回調的位置參數檢索最終調整的播放位置。

   這一點很重要，因為在搜索之後的實際開始位置可能與請求的位置不同。 如果搜索或其他重新定位結束於廣告中斷或跳過廣告中斷，則可能會影響播放行為。

1. 在顯示查找清理欄時使用位置資訊。

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**尋找示例**

在本例中，用戶將搜索條掃描到所需位置。

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
