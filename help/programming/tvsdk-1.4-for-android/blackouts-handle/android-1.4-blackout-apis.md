---
description: 您可以處理即時視訊串流中的中斷，並在中斷期間提供替代內容。
title: 中斷API元素
exl-id: 8e4f1dc3-f2f6-4db9-b9d0-3e79d21032e9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 中斷API元素{#blackout-api-elements}

您可以處理即時視訊串流中的中斷，並在中斷期間提供替代內容。

當即時資料流中發生中斷時，您的播放器會使用事件處理常式來偵測中斷，並為不符合觀看主要資料流資格的使用者提供替代內容。 您的播放器會偵測中斷期間的開始和結束，將播放從主要資料流切換至替代資料流，並在中斷期間結束時切換回主要資料流。

若要處理即時資料流中的中斷：

1. 訂閱即時資料流資訊清單中的中斷標籤，將應用程式設定為偵測中斷標籤。

   TVSDK本身不會偵測中斷標籤；您必須訂閱中斷標籤，才能在資訊清單檔案剖析期間遇到標籤時收到通知。
1. 為您的播放器訂閱的標籤（在此例中為「播放」和「中斷」標籤）建立事件接聽程式。

   當標籤發生時，您的播放器已訂閱前景（主要內容）或背景（替代內容）資料流資訊清單（例如，中斷標籤），TVSDK就會傳送 `TimedMetadataEvent` 並建立 `TimedMetadataObject` 的 `TimedMetadataEvent`.

1. 針對前景和背景資料流的計時中繼資料事件，實作處理常式。

   在這些處理常式中，從定時中繼資料事件物件取得中斷期間的開始和結束時間。
1. 建立用於在中斷期間開始和結束時切換內容的方法。

   當中斷期間開始時，請將主要內容切換到背景，並將替代內容切換到主要資料流。 繼續擷取並剖析背景中的原始資訊清單，並持續檢查「中斷結束」標籤，讓播放器可以在中斷結束時重新加入原始資料流。
1. 如果播放資料流上的中斷範圍在DVR中，請更新不可搜尋的範圍。

   追蹤並處理 `TimedMetadata` 在背景資料流中，透過準備和更新不可搜尋的中斷範圍。

TVSDK提供API元素，這些元素在實施中斷時很有用，包括方法、中繼資料和通知。

在播放器中實作中斷解決方案時，您可以使用下列專案。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 將目前載入的資源儲存為背景資源。 若 `replaceCurrentResource` 此方法之後呼叫，TVSDK會繼續下載背景專案的資訊清單，直到您呼叫 `unregisterCurrentBackgroundItem`， `release`，或 `reset`.

   * `unregisterCurrentBackgroundItem` 將背景專案設定為null並停止擷取和分析背景資訊清單。

* **BlackoutMetadata** -

   特定於中斷的中繼資料類別。

   這可讓您設定無法搜尋的範圍(一系列 `TimeRanges`)。 TVSDK會在每次使用者搜尋時檢查這些範圍。 如果已設定，且使用者搜尋到無法搜尋的範圍，TVSDK會強制檢視器搜尋到無法搜尋範圍的結尾。

* **從這裡開始下一個AdvertisingMetadata** 透過設定在即時資料流上啟用或停用前置滾動 `enableLivePreroll` 為true或false。 若為false，TVSDK不會在內容播放前對前段廣告發出明確廣告伺服器呼叫，因此不會播放前段廣告。 這對中間卷沒有影響。 預設值為true。

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem`  — 在背景資訊清單中偵測到訂閱的標籤和新的時傳送 `TimedMetadata` 執行個體已從中準備。 此 `TimedMetadata` 執行個體會作為引數傳送。

   * `onBackgroundManifestFailed`  — 當媒體播放器完全無法載入背景資訊清單時傳送，也就是說，所有串流URL都會傳回錯誤或無效的回應。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代碼： 204000
      * 型別：警告
      * 背景資訊清單下載發生錯誤。
