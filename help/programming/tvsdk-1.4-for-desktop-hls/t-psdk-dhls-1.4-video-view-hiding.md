---
description: 在使用MediaPlayer檢視播放視訊後，您可以使用TVSDK方法或手動方式隱藏視訊並再次顯示。
title: 隱藏視訊檢視
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 隱藏視訊檢視{#hide-a-video-view}

在使用MediaPlayer檢視播放視訊後，您可以使用TVSDK方法或手動方式隱藏視訊並再次顯示。

您必須先暫停視訊，才能清除視訊或將視訊從顯示畫面移動。
* 選項1：清除視訊影格，使用 `MediaPlayer.clearVideo`並&#x200B;稍後取代框架。
   * 暫停您要隱藏的視訊。
   * 透過呼叫來移除顯示的視訊影格 `MediaPlayer.clearVideo`.
   * 重設 `MediaPlayer` 以便再次播放，請呼叫 `replaceCurrentResource` 或 `replaceCurrentItem`.
* 選項2：移動 `MediaPlayer` 從熒幕檢視，稍後再移回，無需更換。
   * 暫停您要隱藏的視訊。
   * 將檢視移出舞台。 例如：

     ```
     view.x = -300; 
     view.y = -300;
     ```

   * 若要再次顯示視訊，請將檢視移回舞台。
