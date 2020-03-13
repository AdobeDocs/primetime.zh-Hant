---
description: 當您重設MediaPlayer例項時，它會傳回至MediaPlayerState中定義的未初始化IDLE狀態。
seo-description: 當您重設MediaPlayer例項時，它會傳回至MediaPlayerState中定義的未初始化IDLE狀態。
seo-title: 重設或重複使用MediaPlayer例項
title: 重設或重複使用MediaPlayer例項
uuid: 72cc4511-8ab0-44e5-b93c-b36f0321bba8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 重設、重複使用或移除MediaPlayer例項 {#reset-or-reuse-a-mediaplayer-instance}

您可以重設、重複使用或發行您不再需要的MediaPlayer例項。

當您重設MediaPlayer例項時，它會傳回至MediaPlayerState中定義的未初始化IDLE狀態。

此操作在以下情況下非常有用：

* 您想要重複使用 `MediaPlayer` 例項，但需要載入新 `MediaResource` （視訊內容）並取代先前的例項。

   重設可讓您重複使用例 `MediaPlayer` 項，而不需要釋放資源、重新建立資 `MediaPlayer`源和重新分配資源。

* 當處 `MediaPlayer` 於ERROR狀態且需要清除時。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態恢復的唯一方法。

1. 呼叫 `reset` 以將實 `MediaPlayer` 例返回到未初始化狀態：

   ```java
   void reset() throws IllegalStateException; 
   ```

1. 使用 `MediaPlayer.replaceCurrentResource` 載入另一個 `MediaResource`。

   >[!TIP]
   >
   >若要清除錯誤，請載入相同的錯誤 `MediaResource`。

1. 當您收到具有PREPARED `STATUS_CHANGED` 狀態的事件回呼時，請啟動播放。

## 發行MediaPlayer實例和資源{#release-a-mediaplayer-instance-and-resources}

當您不再需要MediaResource時，應該發行MediaPlayer實例和資源。

釋放對象時， `MediaPlayer` 將取消分配與此對象關聯的基 `MediaPlayer` 礎硬體資源。

以下是發行MediaPlayer的一些理由：

* 保留不必要的資源可能會影響效能。
* 留下不必要 `MediaPlayer` 的物件可導致行動裝置持續耗電。
* 如果裝置不支援同一視訊codec的多個執行個體，其他應用程式可能會發生播放失敗。

1. 釋放 `MediaPlayer`。

   ```java
   void release() throws IllegalStateException;
   ```

發佈 `MediaPlayer` 實例後，您無法再使用它。 如果介面的任 `MediaPlayer` 何方法在發佈後被調用，則會 `IllegalStateException` 拋出。