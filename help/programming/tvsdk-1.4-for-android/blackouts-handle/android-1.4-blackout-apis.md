---
description: 您可以處理即時視頻流中的封鎖，並在封鎖期間提供備用內容。
title: 封鎖API元素
exl-id: 8e4f1dc3-f2f6-4db9-b9d0-3e79d21032e9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 封鎖API元素{#blackout-api-elements}

您可以處理即時視頻流中的封鎖，並在封鎖期間提供備用內容。

當即時流中發生封鎖時，您的播放器使用事件處理程式來檢測封鎖，並為那些不適合觀看主流的用戶提供備用內容。 播放器檢測封鎖期的開始和結束，將回放從主流切換到備用流，並在封鎖期結束時切換回主流。

要處理即時流中的封鎖：

1. 通過訂閱即時流清單中的封鎖標籤，設定應用以檢測封鎖標籤。

   TVSDK本身不檢測封鎖標籤；在清單檔案分析過程中遇到標籤時，必須訂閱封鎖標籤才能接收通知。
1. 為播放器訂閱的標籤建立事件偵聽器（在本例中為PLAYBACK和LACUTES標籤）。

   當播放器在前景（主內容）或背景（備用內容）流清單中訂閱（例如，封鎖標籤）的標籤出現時，TVSDK將調度 `TimedMetadataEvent` 建立 `TimedMetadataObject` 為 `TimedMetadataEvent`。

1. 為前台和後台流的定時元資料事件實現處理程式。

   在這些處理程式中，從定時元資料事件對象獲取封鎖期的開始和結束時間。
1. 建立用於在封鎖期開始和結束時切換內容的方法。

   當封鎖期開始時，將主內容切換到後台，將備用內容切換為主流。 繼續提取並分析背景中的原始清單，並繼續檢查「封鎖結束」標籤，以便播放器可以在封鎖結束時重新加入原始流。
1. 如果封鎖範圍在播放流的DVR中，則更新不可查找的範圍。

   跟蹤並處理 `TimedMetadata` 在後台流上，通過準備和更新封鎖不可見範圍。

TVSDK提供在實施封鎖期（包括方法、元資料和通知）時有用的API元素。

在播放器中實施封鎖解決方案時，可以使用以下方法。

* **媒體播放器**

   * `registerCurrentItemAsBackgroundItem` 將當前載入的資源另存為後台資源。 如果 `replaceCurrentResource` 在此方法之後調用，TVSDK將繼續下載後台項的清單，直到您調用 `unregisterCurrentBackgroundItem`。 `release`或 `reset`。

   * `unregisterCurrentBackgroundItem` 將後台項設定為Null，並停止讀取和分析後台清單。

* **封鎖元資料** -

   特定於封鎖的元資料類。

   這允許您設定不可查找的範圍( `TimeRanges`)。 TVSDK每次用戶查找時都檢查這些範圍。 如果設定了它，並且用戶尋求進入不可見範圍，則TVSDK強制查看器到不可見範圍的末尾。

* **從此處開始下一個廣告元資料** 通過設定在即時流上啟用或禁用預卷 `enableLivePreroll` 是真是假。 如果為false，則TVSDK在播放內容之前不會對預播廣告進行顯式廣告伺服器調用，因此不會播放預播。 這對中間輥沒有影響。 預設值為true。

* **MediaPlayer.LacutesEventListener**

   * `onTimedMetadataInBackgroundItem`  — 在檢測到後台清單中的訂閱標籤和新標籤時派送 `TimedMetadata` 實例是從它準備的。 的 `TimedMetadata` 實例作為參數派發。

   * `onBackgroundManifestFailed`  — 當媒體播放器完全無法載入後台清單時調度，即所有流URL返回錯誤或無效響應。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代碼：204000
      * 類型：警告
      * 後台清單下載時出錯。
