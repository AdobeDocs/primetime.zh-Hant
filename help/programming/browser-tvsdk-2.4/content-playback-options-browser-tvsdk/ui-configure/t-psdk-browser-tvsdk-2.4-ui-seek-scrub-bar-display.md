---
description: 在瀏覽器TVSDK中，您可以搜尋資料流中的特定位置（時間）。 串流可以是滑動視窗播放清單或隨選影片(VOD)內容。
title: 使用搜尋列時處理搜尋
exl-id: 4c09b218-917a-4318-82b0-c221d450a2c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 使用搜尋列時處理搜尋{#handle-seek-when-using-the-seek-bar}

在瀏覽器TVSDK中，您可以搜尋資料流中的特定位置（時間）。 串流可以是滑動視窗播放清單或隨選影片(VOD)內容。

>[!IMPORTANT]
>
>只有DVR才允許搜尋即時資料流。

1. 等候瀏覽器TVSDK處於有效的搜尋狀態。

   有效狀態為「已準備」、「完成」、「已暫停」和「正在播放」。 處於有效狀態可確保媒體資源已成功載入。 如果播放器不是處於有效的可搜尋狀態，嘗試呼叫以下方法會擲回 `IllegalStateException`.

   例如，您可以等候瀏覽器TVSDK觸發  `AdobePSDK.MediaPlayerStatusChangeEvent`  具有 `event.status` 之 `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. 將請求的搜尋位置傳遞至 `MediaPlayer.seek` 方法（以毫秒為單位）。

   這會將播放磁頭移動到串流中的不同位置。

   >[!TIP]
   >
   >要求的搜尋位置可能與實際計算的位置不一致。

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. 等候瀏覽器TVSDK觸發  `AdobePSDK.PSDKEventType.SEEK_END`  事件，這會傳回事件中 `actualPosition` 屬性：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   這很重要，因為搜尋之後的實際開始位置可能與要求的位置不同。 可能適用下列部分規則：

   * 如果搜尋或其他重新定位在廣告插播中途結束，或略過廣告插播，則播放行為會受到影響。
   * 您只能搜尋資產的可搜尋持續時間。 若為VOD，即從0到資產的持續時間。

1. 對於在上述範例中建立的搜尋列，請接聽 `setPositionChangeListener()` 若要檢視使用者何時拖曳：

   ```js
   seekBar.setPositionChangeListener(function (pos) { 
                   var range = player.seekableRange; 
                   if (range) { 
                       var duration = range.duration; 
                       var time = duration * pos; // seek bar range is [0,1] 
                       player.seek(time); 
   
                       console.log("seek to " + time + " / " + duration); 
                   } 
   
               }); 
   ```

1. 設定使用者搜尋活動變更的事件接聽程式回呼。

       搜尋作業為非同步，因此瀏覽器TVSDK會傳送這些與搜尋相關的事件：
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` 表示搜尋正在開始。
   * `AdobePSDK.PSDKEventType.SEEK_END` 表示搜尋成功。
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` 表示媒體播放器已重新調整使用者提供的搜尋位置。
