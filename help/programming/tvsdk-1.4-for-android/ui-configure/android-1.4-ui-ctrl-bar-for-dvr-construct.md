---
description: 您可以實現一個支援DVR的控制欄，用於VOD和即時流。 DVR支援包括可查看窗口和客戶端即時點的概念。
title: 構造增強的DVR控制條
exl-id: a812f2d5-f1ee-4df6-9cc7-e39f55ec26f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 構造增強的DVR控制條{#construct-a-control-bar-enhanced-for-dvr}

您可以實現一個支援DVR的控制欄，用於VOD和即時流。 DVR支援包括可查看窗口和客戶端即時點的概念。

* 對於VOD，可瀏覽窗口的長度是整個資產的持續時間。
* 對於即時流，DVR（可查看）窗口的長度定義為從即時播放窗口開始到客戶端即時點結束的時間範圍。

   通過從即時窗口端減去緩衝長度計算客戶機即時點。 目標持續時間是大於或等於清單中片段的最大持續時間的值。

   預設值為10000毫秒。

   用於即時回放的控制條通過在開始回放時首先將拇指定位在客戶端即時點上，並通過顯示標籤不允許查找的區域的區域來支援DVR。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. 要實現具有DVR支援的控制欄，請執行顯示查找擦除欄的步驟，但有幾點小的不同：

   * 您可以選擇實現僅針對可查找範圍而不是回放範圍映射的控制欄。 任何用於搜索的用戶交互都可以被認為在可搜索範圍內是安全的。
   * 您可以選擇實現一個控制欄，該控制欄映射為播放範圍，但也顯示可查找的範圍。

      對於控制欄：
   1. 向表示回放範圍的控制欄添加覆蓋。
   1. 當用戶開始尋道時，使用 `MediaPlayer.getSeekableRange`。

      例如：

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      您還可以選擇使用 `MediaPlayer.LIVE_POINT` 常數。

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
