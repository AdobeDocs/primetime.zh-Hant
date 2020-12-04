---
description: 您可以實作具有VOD和即時串流DVR支援的控制列。 DVR支援包括可檢視視窗和用戶端即時點的概念。
seo-description: 您可以實作具有VOD和即時串流DVR支援的控制列。 DVR支援包括可檢視視窗和用戶端即時點的概念。
seo-title: 構建用於DVR的增強控制條
title: 構建用於DVR的增強控制條
uuid: 08f943e8-90da-4860-92dd-dd289fd68cba
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# 構建增強的DVR控制條{#construct-a-control-bar-enhanced-for-dvr}

您可以實作具有VOD和即時串流DVR支援的控制列。 DVR支援包括可檢視視窗和用戶端即時點的概念。

* 對於VOD，可檢視視窗的長度是整個資產的期間。
* 對於即時串流，DVR（可設定）視窗的長度會定義為從即時播放視窗開始到用戶端即時點結束的時間範圍。

   用戶端即時點是透過從即時視窗端減去緩衝長度來計算。 目標持續時間是大於或等於清單中片段的最大持續時間的值。

   預設值為10000毫秒。

   用於即時回放的控制條通過首先在開始回放時將拇指定位在客戶端即時點以及通過顯示標籤不允許搜索的區域來支援DVR。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. 若要實作具有DVR支援的控制列，請依照顯示搜尋拖曳列的步驟進行，但有一些小差異：

   * 您可以選擇實作僅針對可查找範圍而非播放範圍映射的控制列。 任何用於搜尋的使用者互動都可視為可搜尋範圍內的安全。
   * 您可以選擇實作一個控制列，該控制列已映射為播放範圍，但也會顯示可查看的範圍。

      對於控制列：
   1. 新增覆蓋至代表播放範圍的控制列。
   1. 當使用者開始搜尋時，使用`MediaPlayer.seekableRange`屬性檢查所要的搜尋位置是否在可搜尋範圍內。

      例如：

      ```
      var desiredPosition:Number = // TODO : choose a value 
      
      private function onStatusChange(event:MediaPlayerStatusChangeEvent):void { 
          switch(event.status) { 
              case MediaPlayerStatus.PREPARED: 
                  _mediaPlayer.prepareToPlay(desiredPosition); 
          } 
      }
      ```

      您也可以選擇使用`MediaPlayer.LIVE_POINT`常數尋找用戶端即時點。

      ```
      private function onSeekToLiveClick(event:MouseEvent):void { 
          _player.seek(DefaultMediaPlayer.LIVE_POINT); 
      }
      ```


