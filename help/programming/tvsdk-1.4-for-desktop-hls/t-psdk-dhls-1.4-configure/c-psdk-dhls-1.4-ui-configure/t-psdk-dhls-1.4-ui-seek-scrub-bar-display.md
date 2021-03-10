---
description: TVSDK支援搜尋特定位置（時間），其中串流為隨選視訊(VOD)和即時串流中的滑動視窗播放清單。
title: 顯示具有當前回放位置的查找拖曳條
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# 顯示具有當前回放位置的搜索拖曳條{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支援搜尋特定位置（時間），其中串流為隨選視訊(VOD)和即時串流中的滑動視窗播放清單。

>[!IMPORTANT]
>
>在即時串流中搜尋僅允許DVR使用。

1. 設定搜索回呼。

       搜尋是非同步的，因此TVSDK會調派下列搜尋相關事件：
   
   * `SeekEvent.SEEK_BEGIN` -尋求開始。
   * `SeekEvent.SEEK_END` -尋求成功。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` -重新調整了用戶提供的搜索位置。

1. 等待播放器處於有效狀態以進行搜尋。

   有效狀態包括「已準備」、「已完成」、「暫停」和「正在播放」。

1. 監聽適當事件，以查看使用者在何時清理。
1. 將請求的尋道位置（毫秒）傳遞至`MediaPlayer.seek`方法。

   ```
   function seek(position:Number):void;
   ```

   您只能在資產可見的期間內搜尋。 對於隨選視訊，持續時間從0到資產的持續時間。

   >[!TIP]
   >
   >這會將播放磁頭移動到流中的新位置，但最終計算位置可能與指定的搜索位置不同。

1. 等待TVSDK派單`SeekEvent.SEEK_END`事件。
1. 使用event.actualPosition擷取最終調整的播放位置。

       這很重要，因為搜尋後的實際開始位置可能與請求的位置不同。各種規則可能適用，包括：
   
   * 如果搜尋或其他重新定位在廣告插播的中間結束或跳過廣告插播，則播放行為會受到影響。
   * 如果在段邊界附近尋找，則尋找位置將調整為段的開頭。

1. 在顯示搜尋拖曳列時使用位置資訊。
