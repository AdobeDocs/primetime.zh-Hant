---
description: 在使用MediaPlayer檢視來播放視訊後，您可以使用TVSDK方法或手動隱藏並再次顯示視訊。
seo-description: 在使用MediaPlayer檢視來播放視訊後，您可以使用TVSDK方法或手動隱藏並再次顯示視訊。
seo-title: 隱藏視訊檢視
title: 隱藏視訊檢視
uuid: 7cc02bf4-41ee-4af0-98ba-df070b50b88d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 隱藏視訊檢視{#hide-a-video-view}

在使用MediaPlayer檢視來播放視訊後，您可以使用TVSDK方法或手動隱藏並再次顯示視訊。

您必須先暫停視訊，才能將其清除或從顯示器移除。
* 選項1:使用清除視訊影 `MediaPlayer.clearVideo`格，&#x200B;稍後更換影格。
   * 暫停您要隱藏的影片。
   * 呼叫移除顯示的視訊影格 `MediaPlayer.clearVideo`。
   * 若要重設 `MediaPlayer` 以便再次播放，請呼叫 `replaceCurrentResource` 或 `replaceCurrentItem`。
* 選項2:將檢視 `MediaPlayer` 移離螢幕，稍後再將它移回畫面，而不需加以取代。
   * 暫停您要隱藏的影片。
   * 將檢視移出舞台。 例如：

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * 若要再次顯示視訊，請將檢視移回舞台。
