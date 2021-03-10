---
description: 您可以使用TVSDK來擷取可顯示在搜尋列上之媒體的相關資訊。
title: 顯示視訊的持續時間、目前時間和剩餘時間
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 顯示視訊的持續時間、目前時間和剩餘時間{#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK來擷取可顯示在搜尋列上之媒體的相關資訊。

1. 等待您的播放器處於「已初始化」狀態。
1. 使用`MediaPlayer.currentTime`屬性擷取目前的播放磁頭時間。

   如此可傳回虛擬時間軸上目前播放磁頭的位置（以毫秒為單位）。 時間會相對於可能包含多個替代內容例項的已解析串流來計算，例如，多個廣告或廣告片段會拼接到主串流中。 對於即時／線性串流，傳回的時間一律在播放視窗範圍內。

   ```
   function get currentTime():Number;
   ```

1. 擷取串流的播放範圍並決定持續時間。
   1. 使用`mediaPlayer.playbackRange`屬性來取得虛擬時間軸時間範圍。

      ```
      function get playbackRange():TimeRange;
      ```

   1. 使用`mediacore.utils.TimeRange`剖析時間範圍。
   1. 要確定持續時間，請從範圍結束處減去開始。

      這包括插入至串流（廣告）的其他內容的持續時間。

      對於VOD，範圍一律以零開始，而結束值等於主要內容持續時間與插入串流（廣告）中之其他內容的持續時間之和。

      對於線性／即時資產，範圍代表播放視窗範圍，而此範圍在播放期間會變更。

      TVSDK會派單`MediaPlayerItemEvent.ITEM_UPDATED`事件，指出媒體項目已重新整理，且其屬性（包括播放範圍）已更新。

1. 使用FlexSDK中公開提供的`MediaPlayer`和`HSlider`類別上可用的方法來設定搜尋列參數。

1. 使用計時器定期檢索當前時間並更新`SeekBar`。
