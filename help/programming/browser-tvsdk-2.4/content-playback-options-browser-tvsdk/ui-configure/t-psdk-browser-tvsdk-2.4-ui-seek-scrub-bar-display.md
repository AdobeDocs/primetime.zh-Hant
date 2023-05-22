---
description: 在瀏覽器TVSDK中，可以查找流中的特定位置（時間）。 流可以是滑動窗口播放清單或視頻點播(VOD)內容。
title: 使用查找欄時處理查找
exl-id: 4c09b218-917a-4318-82b0-c221d450a2c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 使用查找欄時處理查找{#handle-seek-when-using-the-seek-bar}

在瀏覽器TVSDK中，可以查找流中的特定位置（時間）。 流可以是滑動窗口播放清單或視頻點播(VOD)內容。

>[!IMPORTANT]
>
>只允許DVR在即時流中查找。

1. 等待瀏覽器TVSDK處於有效狀態進行查找。

   有效狀態包括PREPARED、COMPLETE、PAUSED和PLAYING。 處於有效狀態可確保媒體資源已成功載入。 如果播放器未處於有效可查找狀態，則嘗試調用以下方法將引發 `IllegalStateException`。

   例如，您可以等待瀏覽器TVSDK觸發  `AdobePSDK.MediaPlayerStatusChangeEvent`  和 `event.status` 共 `AdobePSDK.MediaPlayerStatus.PREPARED`。

1. 將請求的尋道位置傳遞到 `MediaPlayer.seek` 方法，以毫秒為單位。

   這將播放頭移動到流中的不同位置。

   >[!TIP]
   >
   >請求的查找位置可能與實際計算位置不一致。

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. 等待瀏覽器TVSDK觸發  `AdobePSDK.PSDKEventType.SEEK_END`  事件，返回事件中的調整位置 `actualPosition` 屬性：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   這一點很重要，因為在搜索後的實際開始位置可能與請求的位置不同。 以下一些規則可能適用：

   * 如果搜索或其他重新定位結束於廣告中斷或跳過廣告中斷，則播放行為會受到影響。
   * 您只能在資產的可尋的持續時間內查找。 對於VOD，從0到資產的持續時間。

1. 對於在上例中建立的搜索欄，請偵聽 `setPositionChangeListener()` 查看用戶正在清理的時間：

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

1. 設定事件偵聽器回調用戶查找活動中的更改。

       查找操作是非同步的，因此瀏覽器TVSDK會調度與查找相關的以下事件：
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` 表示正在開始尋道。
   * `AdobePSDK.PSDKEventType.SEEK_END` 來表明尋找成功。
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` 指示媒體播放器已經調整了由用戶提供的查找位置。
