---
description: 當您重設MediaPlayer執行個體時，它會回到其未初始化的IDLE狀態，如MediaPlayerState中所定義。
title: 重設或重複使用MediaPlayer執行個體
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# 重設、重複使用或移除MediaPlayer執行個體 {#reset-or-reuse-a-mediaplayer-instance}

您可以重設、重複使用或釋放不再需要的MediaPlayer執行個體。

當您重設MediaPlayer執行個體時，它會回到其未初始化的IDLE狀態，如MediaPlayerState中所定義。

此作業在下列情況下相當實用：

* 您想要重複使用 `MediaPlayer` 執行個體，但需要載入新的 `MediaResource` （視訊內容）並取代上一個例項。

  重設可讓您重複使用 `MediaPlayer` 執行環境，無需核發資源，重新建立 `MediaPlayer`，並重新分配資源。

* 當 `MediaPlayer` 處於ERROR狀態，需要清除。

  >[!IMPORTANT]
  >
  >這是從ERROR狀態復原的唯一方法。

1. 呼叫 `reset` 以傳回 `MediaPlayer` 執行個體變更為其未初始化狀態：

   ```java
   void reset() throws IllegalStateException; 
   ```

1. 使用 `MediaPlayer.replaceCurrentResource` 以載入另一個 `MediaResource`.

   >[!TIP]
   >
   >若要清除錯誤，請載入相同的 `MediaResource`.

1. 當您收到 `STATUS_CHANGED` 事件回呼具有PREPARED狀態，請開始播放。

## 發行MediaPlayer例項和資源{#release-a-mediaplayer-instance-and-resources}

當您不再需要MediaResource時，應該發行MediaPlayer例項和資源。

當您發行 `MediaPlayer` 物件，與此物件關聯的基本硬體資源 `MediaPlayer` 物件會取消配置。

以下是發行MediaPlayer的一些理由：

* 保留不必要的資源可能會影響效能。
* 留下不必要的 `MediaPlayer` 物件可能會導致行動裝置持續消耗電池。
* 如果裝置不支援相同視訊轉碼器的多個執行個體，其他應用程式可能會發生播放失敗。

1. 發行 `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

在 `MediaPlayer` 例項已發行，您無法再使用。 若有任何方法屬於 `MediaPlayer` 介面在發行後呼叫，透過 `IllegalStateException` 擲回。
