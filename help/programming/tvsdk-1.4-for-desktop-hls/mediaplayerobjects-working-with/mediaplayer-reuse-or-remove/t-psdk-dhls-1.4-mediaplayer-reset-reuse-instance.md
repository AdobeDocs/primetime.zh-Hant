---
description: 重置MediaPlayer實例時，它將返回到MediaPlayerStatus中定義的未初始化的IDLE狀態。
title: 重置或重用MediaPlayer實例
exl-id: e06a0052-ce0a-4a6c-8ebc-0666b109cf07
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 重置或重用MediaPlayer實例{#reset-or-reuse-a-mediaplayer-instance}

您可以重置、重用或釋放不再需要的MediaPlayer實例。

重置MediaPlayer實例時，它將返回到MediaPlayerStatus中定義的未初始化的IDLE狀態。

此操作在以下情況下非常有用：

* 要重用 `MediaPlayer` 但需要載入新實例 `MediaResource` （視頻內容），並替換上一個實例。

   重置允許重用 `MediaPlayer` 實例，而不需要釋放資源並重新建立 `MediaPlayer`，並重新分配資源。 的 `replaceCurrentItem` 和 `replaceCurrentResource` 方法會自動為您執行這些步驟，而無需調用reset方法。

* 當 `MediaPlayer` 具有錯誤狀態，需要清除。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態恢復的唯一方法。

1. 呼叫 `reset` 返回 `MediaPlayer` 實例到其未初始化狀態：

   ```
   function reset():void; 
   ```

1. 使用 `MediaPlayer.replaceCurrentItem` 或 `MediaPlayer.replaceCurrentResource` 載入 `MediaResource`。

   >[!TIP]
   >
   >要清除錯誤，請載入相同的 `MediaResource`。

1. 當您收到 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 和 `PREPARED` 狀態，開始播放。
