---
description: 您可以實作具有VOD和即時串流DVR支援的控制列。 DVR支援包括可檢視視窗和用戶端即時點的概念。
title: 構建用於DVR的增強控制條
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# 建構DVR {#construct-a-control-bar-enhanced-for-dvr}增強的控制列

您可以實作具有VOD和即時串流DVR支援的控制列。 DVR支援包括可檢視視窗和用戶端即時點的概念。

* 對於VOD，可檢視視窗的長度是整個資產的期間。
* 對於即時串流，DVR（可檢視）視窗的長度會定義為從即時播放視窗開始並在用戶端即時點結束的時間範圍。

   請記住下列資訊：

   * 用戶端即時點是透過從即時視窗端減去緩衝長度來計算。

      目標持續時間是大於或等於清單中片段的最大持續時間的值。
   * 預設值為10000毫秒。
   * 用於即時回放的控制條通過首先在開始回放時將拇指定位在客戶端即時點以及通過顯示標籤不允許搜索的區域來支援DVR。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. 要實施具有DVR支援的控制條，請遵循[顯示具有當前回放位置的搜索拖曳條中的步驟……](../../../tvsdk-2.7-for-android/content-playback-options/ui-configure/t-psdk-android-2.7-ui-seek-scrub-bar-display.md)，但有下列差異：

   * 您可以實作僅針對可尋找範圍（而非播放範圍）映射的控制列。

      任何用於搜尋的使用者互動都可視為可搜尋範圍內的安全。
   * 您可以實作一個控制列，該控制列會對應至播放範圍，但也會顯示可檢視的範圍。

      對於控制列：
   1. 新增覆蓋至代表播放範圍的控制列。
   1. 當用戶開始尋道時，使用`MediaPlayer.getSeekableRange`檢查所需的尋道位置是否在可尋找範圍內。

      例如：

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      您也可以選擇使用`MediaPlayer.LIVE_POINT`常數尋找用戶端即時點。

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```


