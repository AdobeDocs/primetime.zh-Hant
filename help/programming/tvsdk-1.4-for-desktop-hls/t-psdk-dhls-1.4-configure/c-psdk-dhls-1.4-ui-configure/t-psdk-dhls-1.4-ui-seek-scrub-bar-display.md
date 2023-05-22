---
description: TVSDK支援在視頻點播(VOD)和即時流中尋找特定位置（時間），其中流是滑動窗口播放清單。
title: 顯示具有當前回放位置的查找擦除欄
exl-id: a85a06d8-040e-435a-8f55-9df5af3babe1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 顯示具有當前回放位置的查找擦除欄{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支援在視頻點播(VOD)和即時流中尋找特定位置（時間），其中流是滑動窗口播放清單。

>[!IMPORTANT]
>
>只允許DVR在即時流中查找。

1. 設定尋找回調。

       搜索是非同步的，因此TVSDK會調度以下與搜索相關的事件：
   
   * `SeekEvent.SEEK_BEGIN`  — 尋找開始。
   * `SeekEvent.SEEK_END`  — 尋求成功。
   * `SeekEvent.SEEK_POSITION_ADJUSTED`  — 調整用戶提供的查找位置。

1. 等待玩家處於有效狀態以進行查找。

   有效狀態包括PREPARED、COMPLETED、PAUSED和PLAYING。

1. 偵聽相應的事件以查看用戶正在清理的時間。
1. 將請求的查找位置（毫秒）傳遞到 `MediaPlayer.seek` 的雙曲餘切值。

   ```
   function seek(position:Number):void;
   ```

   您只能在資產的可尋的持續時間內查找。 對於視頻點播，持續時間從0到資產的持續時間。

   >[!TIP]
   >
   >這會將播放頭移動到流中的新位置，但最終計算位置可能與指定的查找位置不同。

1. 等待TVSDK派單 `SeekEvent.SEEK_END` 的子菜單。
1. 使用event.actualPosition檢索最終調整的播放位置。

       這一點很重要，因為在搜索之後的實際開始位置可能與請求的位置不同。 可能適用各種規則，包括：
   
   * 如果搜索或其它重新定位結束於廣告中斷或跳過廣告中斷，則播放行為會受到影響。
   * 如果在段邊界附近尋道，則尋道位置將調整為段的開頭。

1. 在顯示查找清理欄時使用位置資訊。
