---
description: 您可以實作具有VOD和即時串流之DVR支援的控制列。 DVR支援包括可搜尋視窗和使用者端即時點的概念。
title: 建構DVR增強的控制列
exl-id: a812f2d5-f1ee-4df6-9cc7-e39f55ec26f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 建構DVR增強的控制列{#construct-a-control-bar-enhanced-for-dvr}

您可以實作具有VOD和即時串流之DVR支援的控制列。 DVR支援包括可搜尋視窗和使用者端即時點的概念。

* 對於VOD，可搜尋視窗的長度是整個資產的持續時間。
* 對於即時串流，DVR （可搜尋）視窗的長度定義為從即時播放視窗開始，並在使用者端即時點結束的時間範圍。

   使用者端即時點的計算方式是從即時視窗結尾減去緩衝長度。 目標持續時間是大於或等於資訊清單中片段最大持續時間的值。

   預設值為10000毫秒。

   即時播放的控制列支援DVR，方法是先在開始播放時將縮圖放置在使用者端即時點，並顯示一個區域，該區域會標籤不允許搜尋的區域。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. 若要實作支援DVR的控制列，請依照顯示搜尋清除列的步驟操作，但有一些細微的差異：

   * 您可以選擇實作僅對應至可搜尋範圍的控制列，而非針對播放範圍的控制列。 搜尋的任何使用者互動都可以視為可搜尋範圍中的安全互動。
   * 您可以選擇實作已對應至播放範圍的控制列，但也會顯示可搜尋範圍。

      對於控制列：
   1. 在代表播放範圍的控制列中新增覆蓋。
   1. 當使用者開始搜尋時，請使用檢查所需的搜尋位置是否在可搜尋範圍內 `MediaPlayer.getSeekableRange`.

      例如：

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      您也可以選擇使用 `MediaPlayer.LIVE_POINT` 常數。

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
