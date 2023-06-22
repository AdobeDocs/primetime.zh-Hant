---
description: 您可以重設、重複使用或釋放不再需要的MediaPlayer執行個體。
title: 重複使用或移除MediaPlayer執行個體
exl-id: 1ee25dd0-95e6-472d-b80c-ef9d8461302d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 重複使用或移除MediaPlayer執行個體 {#reuse-or-remove-a-mediaplayer-instance}

您可以重設、重複使用或釋放不再需要的MediaPlayer執行個體。

## 重設或重複使用MediaPlayer執行個體 {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

當您重設 `MediaPlayer` 執行個體，會回到其未初始化的IDLE狀態，如中所定義 `MediaPlayerStatus`

* 您想要重複使用 `MediaPlayer` 執行個體，但需要載入新的 `MediaResource` （視訊內容）並取代上一個例項。

   重設可讓您重複使用 `MediaPlayer` 執行環境，而不需要核發資源的間接費用，重新建立 `MediaPlayer`，並重新分配資源。

* 當 `MediaPlayer` 處於ERROR狀態，需要清除。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態復原的唯一方法。

   1. 呼叫 `reset` 以傳回 `MediaPlayer` 執行個體變更為其未初始化狀態：

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 使用 `MediaPlayer.replaceCurrentResource()` 以載入另一個 `MediaResource`.

      >[!NOTE]
      >
      >若要清除錯誤，請載入相同的 `MediaResource`.

   1. 當您收到 `STATUS_CHANGED` 事件回撥 `PREPARED` 狀態，開始播放。

## 發行MediaPlayer例項和資源 {#section_13A0914AFF784943ABC343F7EB249C4E}

您應發行 `MediaPlayer` 例項和資源(當您不再需要 `MediaResource`.

當您發行時 `MediaPlayer` 物件，與此物件關聯的基礎硬體資源 `MediaPlayer` 物件會取消配置。

以下是發行「 」的一些理由 `MediaPlayer`：

* 保留不必要的資源可能會影響效能。
* 留下不必要的 `MediaPlayer` 物件例項化可能會導致行動裝置持續消耗電池。
* 如果裝置不支援相同視訊轉碼器的多個執行個體，其他應用程式可能會發生播放失敗。

* 發行 `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >晚於 `MediaPlayer` 執行個體已發行，您無法再使用它。 若有任何方法 `MediaPlayer` 介面在發行後呼叫， `MediaPlayerException` 擲回。
