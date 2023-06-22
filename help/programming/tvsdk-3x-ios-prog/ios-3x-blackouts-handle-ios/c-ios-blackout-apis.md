---
description: TVSDK提供API元素，這些元素在實施中斷時很有用，包括方法、中繼資料和通知。
title: 中斷API元素
exl-id: 76d99d8d-1aae-4faa-aaf2-bb7b535a1c71
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 中斷API元素 {#blackout-api-elements}

TVSDK提供API元素，這些元素在實施中斷時很有用，包括方法、中繼資料和通知。

在播放器中實作中斷解決方案時，您可以使用下列專案。

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 將目前載入的資源儲存為背景資源。 若 `replaceCurrentItemWithPlayerItem` 此方法之後呼叫，TVSDK會繼續下載背景專案的資訊清單，直到您呼叫 `unregisterCurrentBackgroundItem` ， `stop`，或 `reset` .

   * `unregisterCurrentBackgroundItem` 將背景專案設為nil，並停止擷取和分析背景資訊清單。

* **PTMetadata.PTBlackoutMetadata** A `PTMetadata` 中斷的專屬類別。

   這可讓您設定無法搜尋的範圍(一個陣列 `CMTimeRanges`)。 TVSDK會在每次使用者搜尋時檢查這些範圍。 如果已設定，且使用者搜尋到無法搜尋的範圍，TVSDK會強制檢視器搜尋到無法搜尋範圍的結尾。

* **從這裡開始（下一步）** **PTAdMetadata** 透過設定在即時資料流上啟用或停用前置滾動 `enableLivePreroll` 為「是」或「否」。 如果為「否」，TVSDK不會在內容播放之前對前段廣告發出明確廣告伺服器呼叫，因此不會播放前段廣告。 這對中間卷沒有影響。 預設值為YES。

* **NSNotifications**

   * `PTTimedMetadataChangedInBackgroundNotification`  — 當TVSDK偵測到背景資訊清單中的訂閱標籤和新的 `PTTimedMetadata` 執行個體已從中準備。 通知的物件為 `PTMediaPlayerItem` 目前正在播放的執行個體。 您可以擷取 `PTTimedMetadata` 通知的執行個體 `userInfo` 字典使用 `PTTimedMetadataKey` 金鑰。

   * `PTBackgroundManifestErrorNotification`  — 當媒體播放器完全無法載入背景資訊清單時發佈，也就是說，所有串流URL都會傳回錯誤或無效的回應。 通知的物件為 `PTMediaPlayerItem` 目前正在播放的執行個體。

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代碼： 204000
      * 型別：警告
      * 背景資訊清單下載發生錯誤。
   * `INVALID_SEEK_WARNING` 在無法搜尋的範圍內嘗試搜尋時傳送(在 `nonSeekableRanges` 設定於 `PTBlackoutMetadata`)。
