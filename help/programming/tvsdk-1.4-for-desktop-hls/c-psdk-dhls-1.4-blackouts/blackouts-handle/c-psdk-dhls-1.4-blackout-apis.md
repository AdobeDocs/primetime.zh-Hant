---
description: TVSDK提供API元素，這些元素在實施中斷時很有用，包括方法、中繼資料和通知。
title: 中斷API元素
exl-id: 9dae236b-0bd8-4fce-9163-628d4ed94f02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 中斷API元素{#blackout-api-elements}

TVSDK提供API元素，這些元素在實施中斷時很有用，包括方法、中繼資料和通知。

在播放器中實作中斷解決方案時，您可以使用下列專案。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 將目前載入的資源儲存為背景資源。 若 `replaceCurrentResource` 此方法之後呼叫，TVSDK會繼續下載背景專案的資訊清單，直到您呼叫 `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  清除目前設定的背景資源，並停止擷取和分析背景資訊清單。

* **BlackoutMetadata** 特定於中斷的中繼資料型別。

   這可讓您設定無法搜尋的範圍(額外的 `TimeRange` 已呼叫屬性 `nonseekableRange`)。 TVSDK會檢查這些範圍(所需的搜尋位置是否落在 `nonseekableRange`)時。 如果已設定，且使用者搜尋到無法搜尋的範圍，TVSDK會強制檢視器到結尾時間 `seekableRange`.

* **從這裡開始（下一步）** **DefaultMetadataKey** 透過設定在即時資料流上啟用或停用前置滾動 `ENABLE_LIVE_PREROLL` 為true或false。 若為false，TVSDK不會在內容播放前對前段廣告發出明確廣告伺服器呼叫，因此不會播放前段廣告。 這對中間卷沒有影響。 預設值為true。

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 事件子型別 — 當TVSDK在背景資訊清單中偵測到訂閱的標籤時傳送。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代碼： 204000
      * 型別：警告
      * 背景資訊清單下載發生錯誤。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 在無法搜尋的範圍內嘗試搜尋時傳送。
