---
description: 您可以使用TVSDK來擷取可以顯示在搜尋列上的媒體資訊。
title: 顯示視訊的持續時間、目前時間和剩餘時間
exl-id: 490bfa22-6df6-44a3-8e0d-9bb5939ae881
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 顯示視訊的持續時間、目前時間和剩餘時間{#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK來擷取可以顯示在搜尋列上的媒體資訊。

1. 等候播放器處於INITIALIZED狀態。
1. 使用擷取目前的播放點時間 `MediaPlayer.currentTime` 屬性。

   這會傳回虛擬時間軸上目前的播放點位置（以毫秒為單位）。 此時間是相對於已解析資料流來計算的，該資料流可能包含替代內容的多個例項，例如拼接至主資料流的多個廣告或廣告插播。 對於即時/線性串流，傳回的時間一律在播放視窗範圍內。

   ```
   function get currentTime():Number;
   ```

1. 擷取資料流的播放範圍並決定持續時間。
   1. 使用 `mediaPlayer.playbackRange` 屬性以取得虛擬時間軸時間範圍。

      ```
      function get playbackRange():TimeRange;
      ```

   1. 剖析時間範圍，使用 `mediacore.utils.TimeRange`.
   1. 若要判斷持續時間，請從範圍的結尾減去開始時間。

      這包括插入資料流（廣告）中之其他內容的持續時間。

      對於VOD，範圍一律從零開始，而結束值等於主要內容持續時間與插入串流（廣告）中之其他內容持續時間的總和。

      對於線性/即時資產，範圍表示播放視窗範圍，此範圍在播放期間會變更。

      TVSDK會傳送 `MediaPlayerItemEvent.ITEM_UPDATED` 表示媒體專案已重新整理及其屬性（包括播放範圍）已更新的事件。

1. 使用上的可用方法 `MediaPlayer` 和 `HSlider` 在Flex SDK中公開可用以設定搜尋列引數的類別。

1. 使用計時器定期擷取目前時間並更新 `SeekBar`.
