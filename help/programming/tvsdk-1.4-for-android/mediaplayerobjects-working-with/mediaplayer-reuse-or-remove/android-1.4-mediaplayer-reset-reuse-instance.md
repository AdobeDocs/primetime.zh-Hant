---
description: 當您重設MediaPlayer例項時，它會傳回至MediaPlayerState中定義的未初始化IDLE狀態。
seo-description: 當您重設MediaPlayer例項時，它會傳回至MediaPlayerState中定義的未初始化IDLE狀態。
seo-title: 重設或重複使用MediaPlayer例項
title: 重設或重複使用MediaPlayer例項
uuid: 72cc4511-8ab0-44e5-b93c-b36f0321bba8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# 重設、重複使用或移除MediaPlayer例項{#reset-or-reuse-a-mediaplayer-instance}

您可以重設、重複使用或發行您不再需要的MediaPlayer例項。

當您重設MediaPlayer例項時，它會傳回至MediaPlayerState中定義的未初始化IDLE狀態。

此操作在以下情況下非常有用：

* 您想要重複使用`MediaPlayer`例項，但需要載入新的`MediaResource`（視訊內容）並取代先前的例項。

   重設可讓您重複使用`MediaPlayer`例項，而不需釋放資源、重新建立`MediaPlayer`和重新分配資源。

* 當`MediaPlayer`處於ERROR狀態且需要清除時。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態恢復的唯一方法。

1. 調用`reset`將`MediaPlayer`實例返回其未初始化狀態：

   ```java
   void reset() throws IllegalStateException; 
   ```

1. 使用`MediaPlayer.replaceCurrentResource`載入另一個`MediaResource`。

   >[!TIP]
   >
   >要清除錯誤，請載入相同的`MediaResource`。

1. 當您收到`STATUS_CHANGED`事件回呼並且狀態為PREPARED時，請啟動播放。

## 發行MediaPlayer實例和資源{#release-a-mediaplayer-instance-and-resources}

當您不再需要MediaResource時，應該發行MediaPlayer實例和資源。

釋放`MediaPlayer`對象時，將取消分配與此`MediaPlayer`對象關聯的基礎硬體資源。

以下是發行MediaPlayer的一些理由：

* 保留不必要的資源可能會影響效能。
* 留下不必要的`MediaPlayer`物件可持續耗用行動裝置的電池。
* 如果裝置不支援同一視訊codec的多個執行個體，其他應用程式可能會發生播放失敗。

1. 釋放`MediaPlayer`。

   ```java
   void release() throws IllegalStateException;
   ```

在`MediaPlayer`實例發佈後，您無法再使用它。 如果在`MediaPlayer`介面發佈後調用了任何方法，則會拋出`IllegalStateException`。