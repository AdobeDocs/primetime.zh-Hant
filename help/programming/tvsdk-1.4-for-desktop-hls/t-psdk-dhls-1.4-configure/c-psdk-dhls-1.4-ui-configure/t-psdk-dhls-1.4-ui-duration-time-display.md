---
description: 可以使用TVSDK檢索可在查找欄上顯示的媒體資訊。
title: 顯示視頻的持續時間、當前時間和剩餘時間
exl-id: 490bfa22-6df6-44a3-8e0d-9bb5939ae881
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 顯示視頻的持續時間、當前時間和剩餘時間{#display-the-duration-current-time-and-remaining-time-of-the-video}

可以使用TVSDK檢索可在查找欄上顯示的媒體資訊。

1. 等待播放器處於「已初始化」狀態。
1. 使用 `MediaPlayer.currentTime` 屬性。

   這將返回虛擬時間線上當前播放頭位置（毫秒）。 該時間是相對於可能包含多個替代內容實例的解析流計算的，例如，將多個廣告或廣告片段拼接到主流中。 對於即時/線性流，返回的時間始終在回放窗口範圍內。

   ```
   function get currentTime():Number;
   ```

1. 檢索流的播放範圍並確定持續時間。
   1. 使用 `mediaPlayer.playbackRange` 屬性，以獲取虛擬時間軸時間範圍。

      ```
      function get playbackRange():TimeRange;
      ```

   1. 使用 `mediacore.utils.TimeRange`。
   1. 要確定持續時間，請從範圍結束減去開始。

      這包括插入流（廣告）的附加內容的持續時間。

      對於VOD，範圍始終以零開始，結束值等於主內容持續時間和插入流（廣告）中的附加內容的持續時間之和。

      對於線性/即時資產，該範圍表示回放窗口範圍，且此範圍在回放期間會發生更改。

      TVSDK派單 `MediaPlayerItemEvent.ITEM_UPDATED` 事件，指示媒體項已刷新，其屬性（包括播放範圍）已更新。

1. 使用 `MediaPlayer` 和 `HSlider` 可在FlexSDK中公開使用以設定seek-bar參數的類。

1. 使用計時器定期檢索當前時間並更新 `SeekBar`。
