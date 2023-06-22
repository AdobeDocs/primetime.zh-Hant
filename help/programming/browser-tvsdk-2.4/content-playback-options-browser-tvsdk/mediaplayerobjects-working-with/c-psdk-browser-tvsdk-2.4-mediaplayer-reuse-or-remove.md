---
description: 您可以重設、重複使用或釋放不再需要的MediaPlayer執行個體。
title: 重複使用或移除MediaPlayer執行個體
exl-id: 2403e6dd-74c4-43fb-913a-d04e61041628
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# 重複使用或移除MediaPlayer執行個體{#reuse-or-remove-a-mediaplayer-instance}

您可以重設、重複使用或釋放不再需要的MediaPlayer執行個體。

## 重設或重複使用MediaPlayer執行個體 {#section_C183E6164C184C3CBC5321FC6A2528EA}

您可以重設 `MediaPlayer` 執行個體，使其回到未初始化的IDLE狀態，如中所定義 `MediaPlayerStatus`. 您也可以取代目前的媒體專案，或使用先前載入的媒體資源來設定新的媒體專案。

此作業適用於下列情況：

* 您想要重複使用 `MediaPlayer` 執行個體，但需要載入新的 `MediaResource` （視訊內容）並取代上一個例項。

   重設可讓您重複使用 `MediaPlayer` 執行環境，而不需要核發資源的間接費用，重新建立 `MediaPlayer`，並重新分配資源。 此 `replaceCurrentItem` 方法會自動為您執行這些步驟。

* 當 `MediaPlayer` 處於ERROR狀態，需要清除。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態復原的唯一方法。

1. 呼叫 `MediaPlayer.reset()` 以傳回 `MediaPlayer` 執行個體變更為其未初始化狀態：

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. 呼叫 `MediaPlayer.replaceCurrentItem()` 以載入另一個 `MediaResource`

   >[!TIP]
   >
   >若要清除錯誤，請載入相同的 `MediaResource`.

1. 呼叫 `prepareToPlay()` 方法。

   >[!NOTE]
   >
   >當您收到 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 事件具有「已準備」狀態，您可以開始播放。

## 發行MediaPlayer例項和資源 {#section_2D159975C82245098E7078FE0B1578CE}

您應發行 `MediaPlayer` 例項和資源。

以下是發行「 」的一些理由 `MediaPlayer`：

* 保留不必要的資源可能會影響效能。
* 留下不必要的 `MediaPlayer` 物件可能導致行動裝置持續消耗電池。
* 如果裝置不支援相同視訊轉碼器的多個執行個體，其他應用程式可能會發生播放失敗。

* 發行 `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >晚於 `MediaPlayer` 執行個體已發行，您無法再使用它。 若有任何方法 `MediaPlayer` 介面在發行後呼叫，這是 `IllegalStateException` 擲回。
