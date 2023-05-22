---
description: 使用MediaPlayer視圖播放視頻後，可以使用TVSDK方法或手動隱藏並再次顯示視頻。
title: 隱藏視頻視圖
exl-id: 92354cd3-f0ed-4434-a7af-a3545e0e2460
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 隱藏視頻視圖{#hide-a-video-view}

使用MediaPlayer視圖播放視頻後，可以使用TVSDK方法或手動隱藏並再次顯示視頻。

必須先暫停視頻，然後才能清除視頻或將其從顯示器中移動。
* 選項1:清除視頻幀 `MediaPlayer.clearVideo`稍&#x200B;後更換框架。
   * 暫停要隱藏的視頻。
   * 通過呼叫刪除顯示的視頻幀 `MediaPlayer.clearVideo`。
   * 重置 `MediaPlayer` 這樣它就可以再次播放，呼叫 `replaceCurrentResource` 或 `replaceCurrentItem`。
* 選項2:移動 `MediaPlayer` 在螢幕之外查看並稍後將其移回，而無需更換。
   * 暫停要隱藏的視頻。
   * 將視圖移出舞台。 例如：

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * 要再次顯示視頻，請將視圖移回舞台。
