---
description: 當您重設MediaPlayer執行個體時，會如MediaPlayerStatus中所定義，將其傳回至其未初始化的IDLE狀態。
title: 重設或重複使用MediaPlayer執行個體
exl-id: e06a0052-ce0a-4a6c-8ebc-0666b109cf07
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 重設或重複使用MediaPlayer執行個體{#reset-or-reuse-a-mediaplayer-instance}

您可以重設、重複使用或釋放不再需要的MediaPlayer執行個體。

當您重設MediaPlayer執行個體時，會如MediaPlayerStatus中所定義，將其傳回至其未初始化的IDLE狀態。

此作業適用於下列情況：

* 您想要重複使用 `MediaPlayer` 執行個體，但需要載入新的 `MediaResource` （視訊內容）並取代上一個例項。

   重設可讓您重複使用 `MediaPlayer` 執行環境，而不需要核發資源的間接費用，重新建立 `MediaPlayer`，並重新分配資源。 此 `replaceCurrentItem` 和 `replaceCurrentResource` 方法會自動為您執行這些步驟，不必呼叫reset方法。

* 當 `MediaPlayer` 具有ERROR狀態，需要清除。

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
