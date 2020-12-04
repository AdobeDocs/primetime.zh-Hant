---
description: 您可以重設、重複使用或發行您不再需要的MediaPlayer例項。
seo-description: 您可以重設、重複使用或發行您不再需要的MediaPlayer例項。
seo-title: 重複使用或移除MediaPlayer例項
title: 重複使用或移除MediaPlayer例項
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 重複使用或移除MediaPlayer例項{#reuse-or-remove-a-mediaplayer-instance}

您可以重設、重複使用或發行您不再需要的MediaPlayer例項。

## 重設或重複使用MediaPlayer例項{#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

當您重設`MediaPlayer`實例時，該實例將返回到`MediaPlayerStatus`中定義的未初始化的IDLE狀態。

此操作在以下情況下非常有用：

* 您想要重複使用`MediaPlayer`例項，但需要載入新的`MediaResource`（視訊內容）並取代先前的例項。

   重設可讓您重複使用`MediaPlayer`例項，而不需釋放資源、重新建立`MediaPlayer`和重新分配資源。

* 當`MediaPlayer`處於「ERROR（錯誤）」狀態且需要清除時。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態中恢復的唯一方法。

   1. 調用`reset`將`MediaPlayer`實例返回其未初始化狀態：

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 使用`MediaPlayer.replaceCurrentResource()`載入另一個`MediaResource`。

      >[!NOTE]
      >
      >要清除錯誤，請載入相同的`MediaResource`。

   1. 當您收到狀態為`PREPARED`的`STATUS_CHANGED`事件回呼時，請開始播放。

## 發行MediaPlayer實例和資源{#section_13A0914AFF784943ABC343F7EB249C4E}

當您不再需要`MediaResource`時，應釋放`MediaPlayer`實例和資源。

釋放`MediaPlayer`對象時，將取消分配與此`MediaPlayer`對象關聯的基礎硬體資源。

以下是發佈`MediaPlayer`的一些理由：

* 保留不必要的資源可能會影響效能。
* 若保留不必要的`MediaPlayer`物件實例化，可能會持續耗用行動裝置的電池。
* 若有多個例項
裝置上不支援相同視訊codec的視訊，其他應用程式可能會發生播放失敗。

* 釋放`MediaPlayer`。

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >在`MediaPlayer`實例發佈後，您無法再使用它。 如果在`MediaPlayer`介面發佈後調用了任何方法，則會拋出`MediaPlayerException`。