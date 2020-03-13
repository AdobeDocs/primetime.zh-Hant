---
description: 您可以重設、重複使用或發行您不再需要的MediaPlayer例項。
seo-description: 您可以重設、重複使用或發行您不再需要的MediaPlayer例項。
seo-title: 重複使用或移除MediaPlayer例項
title: 重複使用或移除MediaPlayer例項
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 重複使用或移除MediaPlayer例項{#reuse-or-remove-a-mediaplayer-instance}

您可以重設、重複使用或發行您不再需要的MediaPlayer例項。

## 重設或重複使用MediaPlayer例項 {#section_C183E6164C184C3CBC5321FC6A2528EA}

您可以重設一 `MediaPlayer` 個實例，使其返回到其未初始化的IDLE狀態（如中定義） `MediaPlayerStatus`。 您也可以使用先前載入的媒體資源來取代目前的媒體項目或設定新的媒體項目。

此操作在以下情況下非常有用：

* 您想要重複使用 `MediaPlayer` 例項，但需要載入新 `MediaResource` （視訊內容）並取代先前的例項。

   重設可讓您重複使用例 `MediaPlayer` 項，而不需要釋放資源、重新建立資 `MediaPlayer`源和重新分配資源。 方法 `replaceCurrentItem` 會自動為您執行這些步驟。

* 當處 `MediaPlayer` 於ERROR狀態且需要清除時。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態恢復的唯一方法。

1. 呼叫 `MediaPlayer.reset()` 以將實 `MediaPlayer` 例返回到未初始化狀態：

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. 呼叫 `MediaPlayer.replaceCurrentItem()` 以載入另一個 `MediaResource`

   >[!TIP]
   >
   >若要清除錯誤，請載入相同的錯誤 `MediaResource`。

1. 呼叫方 `prepareToPlay()` 法。

   >[!NOTE]
   >
   >當您收到具 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 有PREPARED狀態的事件時，可以開始播放。

## 發行MediaPlayer實例和資源 {#section_2D159975C82245098E7078FE0B1578CE}

當您不再需 `MediaPlayer` 要MediaResource時，應釋放實例和資源。

以下是發佈的一些理由 `MediaPlayer`:

* 保留不必要的資源可能會影響效能。
* 留下不必要 `MediaPlayer` 的物件可導致行動裝置持續耗電。
* 如果裝置不支援同一視訊codec的多個執行個體，其他應用程式可能會發生播放失敗。

* 釋放 `MediaPlayer`。

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >發佈 `MediaPlayer` 實例後，您無法再使用它。 如果介面的任 `MediaPlayer` 何方法在發佈後被調用，則會 `IllegalStateException` 拋出。

