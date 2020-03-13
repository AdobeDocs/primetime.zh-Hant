---
description: TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。
seo-description: TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。
seo-title: 封鎖API元素
title: 封鎖API元素
uuid: 65e1668c-6a19-4910-83a2-46d364e94e5f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 封鎖API元素{#blackout-api-elements}

TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。

在您的播放器中實施封鎖期解決方案時，可使用下列功能。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 將當前載入的資源另存為背景資源。 如果 `replaceCurrentResource` 在此方法後呼叫，TVSDK會持續下載背景項目的資訊清單，直到您呼叫 `unregisterCurrentBackgroundItem`。

   * `unregisterCurrentBackgroundItem`  清除目前設定的背景資源，並停止擷取和剖析背景資訊清單。

* **BlackoutMetadata** —特定於封鎖的元資料類型。

   這可讓您在TVSDK上設定不可見的範圍( `TimeRange` 稱為其 `nonseekableRange`他屬性)。 TVSDK會在使用者每次搜尋時檢查這些範圍(所需的搜尋位 `nonseekableRange`置是否在a內)。 如果已設定，且使用者搜尋至不可檢視的範圍，TVSDK會強制檢視器至終止時間 `seekableRange`。

* **START HERE NEXT** **DefaultMetadataKeys** 透過設定為true或false，在即時串流上啟用或停 `ENABLE_LIVE_PREROLL` 用前置鏡頭。 若為false,TVSDK在內容播放前不會明確呼叫前段廣告的廣告伺服器，因此不會播放前段廣告。 這對中間輥沒有影響。 預設值為true。

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 事件子類型——當TVSDK偵測到背景資訊清單中的訂閱標籤時傳送。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 程式碼：204000
      * 類型：警告
      * 背景資訊清單下載時發生錯誤。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 在不可見範圍內嘗試搜索時發送。


