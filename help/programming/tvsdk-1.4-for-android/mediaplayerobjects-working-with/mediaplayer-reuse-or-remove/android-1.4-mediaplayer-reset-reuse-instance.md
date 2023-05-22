---
description: 重置MediaPlayer實例時，它將返回到MediaPlayerState中定義的未初始化的IDLE狀態。
title: 重置或重用MediaPlayer實例
exl-id: db8264f7-2f33-4441-86db-bb985edf7c3c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# 重置、重用或刪除MediaPlayer實例 {#reset-or-reuse-a-mediaplayer-instance}

您可以重置、重用或釋放不再需要的MediaPlayer實例。

重置MediaPlayer實例時，它將返回到MediaPlayerState中定義的未初始化的IDLE狀態。

此操作在以下情況下非常有用：

* 要重用 `MediaPlayer` 但需要載入新實例 `MediaResource` （視頻內容），並替換上一個實例。

   重置允許重用 `MediaPlayer` 實例，而不需要釋放資源並重新建立 `MediaPlayer`，並重新分配資源。

* 當 `MediaPlayer` 處於ERROR狀態，需要清除。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態恢復的唯一方法。

1. 呼叫 `reset` 返回 `MediaPlayer` 實例到其未初始化狀態：

   ```java
   void reset() throws IllegalStateException; 
   ```

1. 使用 `MediaPlayer.replaceCurrentResource` 載入 `MediaResource`。

   >[!TIP]
   >
   >要清除錯誤，請載入相同的 `MediaResource`。

1. 當您收到 `STATUS_CHANGED` 事件回調（狀態為PREPARED），啟動回放。

## 釋放MediaPlayer實例和資源{#release-a-mediaplayer-instance-and-resources}

在不再需要MediaResource時，應釋放MediaPlayer實例和資源。

當您釋放 `MediaPlayer` 對象，與此關聯的基礎硬體資源 `MediaPlayer` 對象被取消分配。

以下是發佈MediaPlayer的一些原因：

* 保留不必要的資源會影響效能。
* 留下不必要的 `MediaPlayer` 對象可導致移動設備的電池消耗持續。
* 如果一台設備上不支援同一視頻編解碼器的多個實例，則其他應用程式可能會出現回放失敗。

1. 釋放 `MediaPlayer`。

   ```java
   void release() throws IllegalStateException;
   ```

在 `MediaPlayer` 實例已發佈，您不能再使用它。 如果 `MediaPlayer` 介面在發佈後調用， `IllegalStateException` 。
