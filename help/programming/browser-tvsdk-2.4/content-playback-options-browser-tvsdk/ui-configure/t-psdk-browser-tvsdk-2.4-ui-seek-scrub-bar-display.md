---
description: 在瀏覽器TVSDK中，您可以尋找串流中的特定位置（時間）。 串流可以是滑動視窗播放清單或隨選視訊(VOD)內容。
seo-description: 在瀏覽器TVSDK中，您可以尋找串流中的特定位置（時間）。 串流可以是滑動視窗播放清單或隨選視訊(VOD)內容。
seo-title: 使用查找條時處理查找
title: 使用查找條時處理查找
uuid: a7c74141-581f-40a3-9d28-ce56ba56773c
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# 使用尋道列{#handle-seek-when-using-the-seek-bar}時處理尋道

在瀏覽器TVSDK中，您可以尋找串流中的特定位置（時間）。 串流可以是滑動視窗播放清單或隨選視訊(VOD)內容。

>[!IMPORTANT]
>
>在即時串流中搜尋僅允許DVR使用。

1. 等待瀏覽器TVSDK處於有效狀態以進行搜尋。

   有效狀態包括準備、完成、暫停和播放。 處於有效狀態可確保媒體資源已成功載入。 如果播放器未處於有效可查找狀態，嘗試呼叫下列方法會引發`IllegalStateException`。

   例如，您可以等待瀏覽器TVSDK以`event.status`的`AdobePSDK.MediaPlayerStatus.PREPARED`觸發`AdobePSDK.MediaPlayerStatusChangeEvent`。

1. 將請求的尋道位置作為參數傳遞至`MediaPlayer.seek`方法（以毫秒為單位）。

   這會將播放頭移至串流中的不同位置。

   >[!TIP]
   >
   >請求的搜索位置可能與實際計算位置不一致。

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. 等待瀏覽器TVSDK觸發`AdobePSDK.PSDKEventType.SEEK_END`事件，該事件會傳回事件`actualPosition`屬性中調整的位置：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   這很重要，因為搜尋後的實際開始位置可能與要求的位置不同。 下列部分規則可能適用：

   * 如果搜尋或其他重新定位結束於廣告插播的中間或跳過廣告插播，則播放行為會受到影響。
   * 您只能在資產可見的期間內搜尋。 對於VOD，即從0到資產的持續時間。

1. 對於在上述範例中建立的seekbar，請監聽`setPositionChangeListener()`以查看使用者何時正在清除：

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

1. 為用戶的查找活動中的更改設定事件偵聽器回調。

       搜尋操作是非同步的，因此瀏覽器TVSDK會調度這些與搜尋相關的事件：
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` 以指出搜尋正在開始。
   * `AdobePSDK.PSDKEventType.SEEK_END` 表明搜尋成功。
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` 以指出媒體播放器已調整使用者提供的搜尋位置。

