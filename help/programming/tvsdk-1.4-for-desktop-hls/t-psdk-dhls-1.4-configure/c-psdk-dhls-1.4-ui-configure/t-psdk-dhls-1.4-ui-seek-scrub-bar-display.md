---
description: TVSDK支援在隨選視訊(VOD)和即時資料流中，搜尋資料流為滑動視窗播放清單的特定位置（時間）。
title: 顯示具有目前播放位置的搜尋拖曳列
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 顯示具有目前播放位置的搜尋拖曳列{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支援在隨選視訊(VOD)和即時資料流中，搜尋資料流為滑動視窗播放清單的特定位置（時間）。

>[!IMPORTANT]
>
>只有DVR才允許在即時資料流中進行搜尋。

1. 設定搜尋的回呼。

       搜尋為非同步，因此TVSDK會傳送下列搜尋相關事件：
   
   * `SeekEvent.SEEK_BEGIN`  — 搜尋開始。
   * `SeekEvent.SEEK_END`  — 搜尋成功。
   * `SeekEvent.SEEK_POSITION_ADJUSTED`  — 已重新調整使用者提供的搜尋位置。

1. 等候播放器處於有效的搜尋狀態。

   有效的狀態包括「已準備」、「已完成」、「已暫停」和「正在播放」。

1. 聆聽適當的事件，以檢視使用者何時進行清除。
1. 將請求的搜尋位置（毫秒）傳遞至 `MediaPlayer.seek` 方法。

   ```
   function seek(position:Number):void;
   ```

   您只能搜尋資產的可搜尋期間。 對於隨選影片，持續時間是從0到資產的持續時間。

   >[!TIP]
   >
   >這會將播放磁頭移動到串流中的新位置，但最終計算位置可能與指定的搜尋位置不同。

1. 等候TVSDK派遣 `SeekEvent.SEEK_END` 事件。
1. 使用event.actualPosition擷取最終調整後的播放位置。

       這很重要，因為搜尋之後的實際開始位置可能與要求的位置不同。 可能適用各種規則，包括：
   
   * 如果搜尋或其他重新定位在廣告插播中途結束，或略過廣告插播，則會影響播放行為。
   * 如果您在區段邊界附近進行搜尋，會調整搜尋位置至區段的開頭。

1. 顯示搜尋拖曳列時使用位置資訊。
