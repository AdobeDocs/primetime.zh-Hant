---
description: TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。
title: 封鎖API元素
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# 封鎖API元素{#blackout-api-elements}

TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。

在您的播放器中實施封鎖期解決方案時，可使用下列功能。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 將當前載入的資源另存為背景資源。如果在此方法後呼叫`replaceCurrentResource`,TVSDK會繼續下載背景項目的資訊清單，直到您呼叫`unregisterCurrentBackgroundItem`為止。

   * `unregisterCurrentBackgroundItem`  清除目前設定的背景資源，並停止擷取和剖析背景資訊清單。

* **** BlackoutMetadataA特定於封鎖的元資料類型。

   這可讓您在TVSDK上設定不可見的範圍（稱為`nonseekableRange`的其他`TimeRange`屬性）。 TVSDK會在使用者每次搜尋時檢查這些範圍（所需的搜尋位置是否落在`nonseekableRange`內）。 如果已設定，且使用者搜尋至不可見的範圍，TVSDK會強制檢視器至`seekableRange`的結束時間。

* **START HERE** **** NEXTDefaultMetadataKeys透過設定為true或false，在即時串流上啟用或停 `ENABLE_LIVE_PREROLL` 用前置鏡頭。若為false,TVSDK在內容播放前不會明確呼叫前段廣告的廣告伺服器，因此不會播放前段廣告。 這對中間輥沒有影響。 預設值為true。

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 事件子類型——當TVSDK偵測到背景資訊清單中的訂閱標籤時傳送。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 程式碼：204000
      * 類型：警告
      * 背景資訊清單下載時發生錯誤。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 在不可見範圍內嘗試搜索時發送。


