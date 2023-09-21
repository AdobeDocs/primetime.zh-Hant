---
description: 當您重設MediaPlayer執行個體時，它會回到其未初始化的IDLE狀態，如MediaPlayerStatus中所定義。
title: 重設或重複使用MediaPlayer執行個體
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 重設或重複使用MediaPlayer執行個體{#reset-or-reuse-a-mediaplayer-instance}

您可以重設、重複使用或釋放不再需要的MediaPlayer執行個體。

當您重設MediaPlayer執行個體時，它會回到其未初始化的IDLE狀態，如MediaPlayerStatus中所定義。

此作業在下列情況下相當實用：

* 您想要重複使用 `MediaPlayer` 執行個體，但需要載入新的 `MediaResource` （視訊內容）並取代上一個例項。

  重設可讓您重複使用 `MediaPlayer` 執行環境，無需核發資源，重新建立 `MediaPlayer`，並重新分配資源。 此 `replaceCurrentItem` 和 `replaceCurrentResource` 方法會自動為您執行這些步驟，不必呼叫reset方法。

* 當 `MediaPlayer` 狀態為ERROR，需要清除。

  >[!IMPORTANT]
  >
  >這是從ERROR狀態復原的唯一方法。

1. 呼叫 `reset` 以傳回 `MediaPlayer` 執行個體變更為其未初始化狀態：

   ```
   function reset():void; 
   ```

1. 使用 `MediaPlayer.replaceCurrentItem` 或 `MediaPlayer.replaceCurrentResource` 以載入另一個 `MediaResource`.

   >[!TIP]
   >
   >若要清除錯誤，請載入相同的 `MediaResource`.

1. 當您收到 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 使用 `PREPARED` 狀態，開始播放。
