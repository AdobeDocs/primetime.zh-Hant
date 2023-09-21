---
description: 您可以使用TVSDK來擷取可以顯示在搜尋列上的媒體資訊。
title: 顯示視訊的持續時間、目前時間和剩餘時間
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 顯示視訊的持續時間、目前時間和剩餘時間{#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK來擷取可以顯示在搜尋列上的媒體資訊。

1. 等候您的播放器處於「已初始化」狀態。
1. 使用擷取目前的播放點時間 `MediaPlayer.currentTime` 屬性。

   這會傳回虛擬時間軸上目前的播放點位置（以毫秒為單位）。 此時間是相對於已解析資料流而計算的，該資料流可能包含多個替代內容的例項，例如多個廣告或拼接到主資料流中的廣告插播。 對於即時/線性串流，傳回的時間一律在播放視窗範圍內。

   ```
   function get currentTime():Number;
   ```

1. 擷取資料流的播放範圍並決定持續時間。
   1. 使用 `mediaPlayer.playbackRange` 屬性以取得虛擬時間軸時間範圍。

      ```
      function get playbackRange():TimeRange;
      ```

   1. 剖析時間範圍，使用 `mediacore.utils.TimeRange`.
   1. 若要決定持續時間，請從範圍的結尾減去開始時間。

      這包括插入資料流（廣告）中的其他內容持續時間。

      對於VOD，範圍一律從零開始，而結束值等於主要內容持續時間與插入到資料流（廣告）中之其他內容持續時間的和。

      對於線性/即時資產，範圍表示播放視窗範圍，此範圍在播放期間會變更。

      TVSDK傳送 `MediaPlayerItemEvent.ITEM_UPDATED` 表示媒體專案已重新整理及其屬性（包括播放範圍）已更新的事件。

1. 使用上的可用方法 `MediaPlayer` 和 `HSlider` 在Flex SDK中公開可用以設定搜尋列引數的類別。

1. 使用計時器定期擷取目前時間並更新 `SeekBar`.
