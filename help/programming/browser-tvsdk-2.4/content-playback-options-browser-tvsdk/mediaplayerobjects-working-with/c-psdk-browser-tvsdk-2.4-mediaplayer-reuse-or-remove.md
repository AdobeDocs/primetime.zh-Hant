---
description: 您可以重置、重用或釋放不再需要的MediaPlayer實例。
title: 重用或刪除MediaPlayer實例
exl-id: 2403e6dd-74c4-43fb-913a-d04e61041628
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# 重用或刪除MediaPlayer實例{#reuse-or-remove-a-mediaplayer-instance}

您可以重置、重用或釋放不再需要的MediaPlayer實例。

## 重置或重用MediaPlayer實例 {#section_C183E6164C184C3CBC5321FC6A2528EA}

可以重置 `MediaPlayer` 實例，以將其返回到在中定義的未初始化的IDLE狀態 `MediaPlayerStatus`。 您還可以使用先前載入的媒體資源替換當前媒體項目或設定新媒體項目。

此操作在以下情況下非常有用：

* 要重用 `MediaPlayer` 但需要載入新實例 `MediaResource` （視頻內容），並替換上一個實例。

   重置允許重用 `MediaPlayer` 實例，而不需要釋放資源並重新建立 `MediaPlayer`，並重新分配資源。 的 `replaceCurrentItem` 方法會自動為您執行這些步驟。

* 當 `MediaPlayer` 處於ERROR狀態，需要清除。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態恢復的唯一方法。

1. 呼叫 `MediaPlayer.reset()` 返回 `MediaPlayer` 實例到其未初始化狀態：

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. 呼叫 `MediaPlayer.replaceCurrentItem()` 載入 `MediaResource`

   >[!TIP]
   >
   >要清除錯誤，請載入相同的 `MediaResource`。

1. 呼叫 `prepareToPlay()` 的雙曲餘切值。

   >[!NOTE]
   >
   >當您收到 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` PREPARED狀態的事件，可以開始回放。

## 釋放MediaPlayer實例和資源 {#section_2D159975C82245098E7078FE0B1578CE}

你應該釋放 `MediaPlayer` 不再需要MediaResource時的實例和資源。

以下是發佈 `MediaPlayer`:

* 保留不必要的資源會影響效能。
* 留下不必要的 `MediaPlayer` 對象可導致移動設備的電池消耗持續。
* 如果一台設備上不支援同一視頻編解碼器的多個實例，則其他應用程式可能會出現回放失敗。

* 釋放 `MediaPlayer`。

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >在 `MediaPlayer` 實例已發佈，您不能再使用它。 如果 `MediaPlayer` 介面在發佈後調用， `IllegalStateException` 。
