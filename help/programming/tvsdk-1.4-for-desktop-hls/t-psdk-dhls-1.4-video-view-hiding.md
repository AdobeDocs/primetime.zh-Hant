---
description: 在使用MediaPlayer檢視播放視訊後，您可以使用TVSDK方法或手動隱藏視訊並再次顯示。
title: 隱藏視訊檢視
exl-id: 92354cd3-f0ed-4434-a7af-a3545e0e2460
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 隱藏視訊檢視{#hide-a-video-view}

在使用MediaPlayer檢視播放視訊後，您可以使用TVSDK方法或手動隱藏視訊並再次顯示。

您必須先暫停視訊，才能將其清除或將其從顯示區移動。
* 選項1：清除視訊框架，使用 `MediaPlayer.clearVideo`並&#x200B;稍後取代框架。
   * 暫停您要隱藏的視訊。
   * 呼叫，移除顯示的視訊影格 `MediaPlayer.clearVideo`.
   * 重設 `MediaPlayer` 為了能夠再次播放，請呼叫 `replaceCurrentResource` 或 `replaceCurrentItem`.
* 選項2：移動 `MediaPlayer` 從熒幕檢視，稍後再移回來，不必加以取代。
   * 暫停您要隱藏的視訊。
   * 將檢視移出舞台。 例如：

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * 若要再次顯示視訊，請將檢視移回舞台。
