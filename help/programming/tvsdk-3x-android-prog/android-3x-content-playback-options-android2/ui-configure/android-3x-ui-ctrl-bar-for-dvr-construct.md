---
description: 您可以實作具有VOD和即時串流DVR支援的控制列。 DVR支援包括可檢視視窗和用戶端即時點的概念。
seo-description: 您可以實作具有VOD和即時串流DVR支援的控制列。 DVR支援包括可檢視視窗和用戶端即時點的概念。
seo-title: 構建用於DVR的增強控制條
title: 構建用於DVR的增強控制條
uuid: 988dcaf5-896d-4da1-8b78-5acf5a317aa3
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# 構建用於DVR的增強控制條 {#construct-a-control-bar-enhanced-for-dvr}

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

1. 若要實作具有DVR支援的控制列，請依照「顯示具有目前播放位置的尋 [找拖曳列」中的步驟進行。](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md) 有下列差異：

   * 您可以實作僅針對可尋找範圍（而非播放範圍）映射的控制列。

      任何用於搜尋的使用者互動都可視為可搜尋範圍內的安全。
   * 您可以實作一個控制列，該控制列會對應至播放範圍，但也會顯示可檢視的範圍。

      對於控制列：
   1. 新增覆蓋至代表播放範圍的控制列。
   1. 當用戶開始尋道時，使用檢查所需的尋道位置是否在可尋道範圍內 `MediaPlayer.getSeekableRange`。

      例如：

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      您也可以選擇使用常數尋找用戶端即時 `MediaPlayer.LIVE_POINT` 點。

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
