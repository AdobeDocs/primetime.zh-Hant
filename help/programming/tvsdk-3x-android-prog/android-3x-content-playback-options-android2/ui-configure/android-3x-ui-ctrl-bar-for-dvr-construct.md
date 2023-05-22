---
description: 您可以實現一個支援DVR的控制欄，用於VOD和即時流。 DVR支援包括可查看窗口和客戶端即時點的概念。
title: 構造增強的DVR控制條
exl-id: 12e989f3-0e39-4224-89a7-ebfeb130f5fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 構造增強的DVR控制條 {#construct-a-control-bar-enhanced-for-dvr}

您可以實現一個支援DVR的控制欄，用於VOD和即時流。 DVR支援包括可查看窗口和客戶端即時點的概念。

* 對於VOD，可瀏覽窗口的長度是整個資產的持續時間。
* 對於即時流，DVR（可查看）窗口的長度定義為從即時播放窗口開始到客戶端即時點結束的時間範圍。

   記住以下資訊：

   * 通過從即時窗口端減去緩衝長度計算客戶機即時點。

      目標持續時間是大於或等於清單中片段的最大持續時間的值。
   * 預設值為10000毫秒。
   * 用於即時回放的控制條通過在開始回放時首先將拇指定位在客戶端即時點上，並通過顯示標籤不允許查找的區域的區域來支援DVR。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. 要實現具有DVR支援的控制欄，請按照中的步驟操作 [顯示具有當前回放位置的查找擦除欄。](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md) 差異如下：

   * 您可以實現一個控制欄，該控制欄僅映射至可查找範圍，而不映射至回放範圍。

      任何用於搜索的用戶交互都可以被認為在可搜索範圍內是安全的。
   * 您可以實現一個控制欄，該控制欄映射為播放範圍，但也顯示可查找的範圍。

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
