---
description: 您可以實作對VOD和即時串流具有DVR支援的控制列。 DVR支援包含可檢視視窗和用戶端即時點的概念。
title: 構建增強的DVR控制欄
exl-id: 12e989f3-0e39-4224-89a7-ebfeb130f5fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 構建增強的DVR控制欄 {#construct-a-control-bar-enhanced-for-dvr}

您可以實作對VOD和即時串流具有DVR支援的控制列。 DVR支援包含可檢視視窗和用戶端即時點的概念。

* 對於VOD，可搜尋視窗的長度是整個資產的持續時間。
* 對於即時串流，DVR（可查看）視窗的長度定義為從即時播放視窗開始到用戶端即時點結束的時間範圍。

   請記住以下資訊：

   * 從即時視窗結尾減去緩衝長度，即可計算用戶端即時點。

      目標持續時間值大於或等於資訊清單中片段的最大持續時間。
   * 預設值為10000毫秒。
   * 用於即時播放的控制條通過在開始播放時首先將拇指定位在客戶端即時點，並通過顯示標籤不允許搜索的區域的區域來支援DVR。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. 若要實作具有DVR支援的控制列，請遵循 [使用目前的播放位置顯示搜尋拖曳列。](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md) 差異：

   * 您可以實作僅對應至可搜尋範圍的控制列，而非對於播放範圍。

      在可搜尋範圍內，任何搜尋的使用者互動都可視為安全。
   * 您可以實作已對應播放範圍的控制列，但也會顯示可搜尋的範圍。

      對於控制欄：
   1. 在代表播放範圍的控制列中新增覆蓋。
   1. 當使用者開始搜尋時，請使用 `MediaPlayer.getSeekableRange`.

      例如：

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      您也可以選擇使用來搜尋用戶端即時點 `MediaPlayer.LIVE_POINT` 常數。

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
