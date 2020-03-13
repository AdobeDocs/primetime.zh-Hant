---
description: 您可以重設、重複使用或發行您不再需要的MediaPlayer例項。
seo-description: 您可以重設、重複使用或發行您不再需要的MediaPlayer例項。
seo-title: 重複使用或移除MediaPlayer例項
title: 重複使用或移除MediaPlayer例項
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 重複使用或移除MediaPlayer例項 {#reuse-or-remove-a-mediaplayer-instance}

您可以重設、重複使用或發行您不再需要的MediaPlayer例項。

## 重設或重複使用MediaPlayer例項 {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

重設實例時， `MediaPlayer` 它將返回其未初始化的IDLE狀態，如中所定義 `MediaPlayerStatus`。

此操作在以下情況下非常有用：

* 您想要重複使用 `MediaPlayer` 例項，但需要載入新 `MediaResource` （視訊內容）並取代先前的例項。

   重設可讓您重複使用例 `MediaPlayer` 項，而不需要釋放資源、重新建立資 `MediaPlayer`源和重新分配資源。

* 當處於 `MediaPlayer` ERROR狀態且需要清除時。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態中恢復的唯一方法。

   1. 呼叫 `reset` 以將實 `MediaPlayer` 例返回其未初始化狀態：

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 使用 `MediaPlayer.replaceCurrentResource()` 載入另一個 `MediaResource`。

      >[!NOTE]
      >
      >若要清除錯誤，請載入相同的錯誤 `MediaResource`。

   1. 當您收到狀態 `STATUS_CHANGED` 的事件回呼 `PREPARED` 時，請開始播放。

## 發行MediaPlayer實例和資源 {#section_13A0914AFF784943ABC343F7EB249C4E}

您應在不再需 `MediaPlayer` 要時釋放實例和資源 `MediaResource`。

釋放對象時， `MediaPlayer` 將取消分配與此對象關聯的基 `MediaPlayer` 礎硬體資源。

以下是發佈的一些理由 `MediaPlayer`:

* 保留不必要的資源可能會影響效能。
* 如果執行個體化不 `MediaPlayer` 必要的物件，可能會持續耗用行動裝置的電池。
* 如果裝置不支援同一視訊codec的多個執行個體，其他應用程式可能會發生播放失敗。

* 釋放 `MediaPlayer`。

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >發佈 `MediaPlayer` 實例後，您無法再使用它。 如果介面的任 `MediaPlayer` 何方法在發佈後被調用，則會 `MediaPlayerException` 拋出。