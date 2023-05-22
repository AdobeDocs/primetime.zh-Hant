---
description: TVSDK提供在實施封鎖期（包括方法、元資料和通知）時有用的API元素。
title: 封鎖API元素
exl-id: 9dae236b-0bd8-4fce-9163-628d4ed94f02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 封鎖API元素{#blackout-api-elements}

TVSDK提供在實施封鎖期（包括方法、元資料和通知）時有用的API元素。

在播放器中實施封鎖解決方案時，可以使用以下方法。

* **媒體播放器**

   * `registerCurrentItemAsBackgroundItem` 將當前載入的資源另存為後台資源。 如果 `replaceCurrentResource` 在此方法之後調用，TVSDK將繼續下載後台項的清單，直到您調用 `unregisterCurrentBackgroundItem`。

   * `unregisterCurrentBackgroundItem`  清除當前設定的後台資源，並停止提取和分析後台清單。

* **封鎖元資料** 特定於封鎖的元資料類型。

   這允許您設定不可見的範圍(附加 `TimeRange` 屬性調用 `nonseekableRange`)。 TVSDK檢查這些範圍(所需的搜索位置是否位於 `nonseekableRange`)。 如果設定了它，並且用戶尋求進入不可查找的範圍，則TVSDK將強制查看者到 `seekableRange`。

* **下一頁開始** **預設元資料鍵** 通過設定在即時流上啟用或禁用預卷 `ENABLE_LIVE_PREROLL` 是真是假。 如果為false，則TVSDK在播放內容之前不會對預播廣告進行顯式廣告伺服器調用，因此不會播放預播。 這對中間輥沒有影響。 預設值為true。

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 事件子類型 — 當TVSDK檢測到後台清單中的訂閱標籤時調度。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代碼：204000
      * 類型：警告
      * 後台清單下載時出錯。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 在不可查範圍內嘗試查找時發送。
