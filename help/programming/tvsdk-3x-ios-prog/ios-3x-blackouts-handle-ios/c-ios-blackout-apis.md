---
description: TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。
seo-description: TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。
seo-title: 封鎖API元素
title: 封鎖API元素
uuid: f87f4ed0-3f97-48bd-bceb-28357a978964
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 封鎖API元素 {#blackout-api-elements}

TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。

在您的播放器中實施封鎖期解決方案時，可使用下列功能。

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 將當前載入的資源另存為背景資源。 如 `replaceCurrentItemWithPlayerItem` 果在此方法後呼叫，TVSDK會繼續下載背景項目的資訊清單，直到您呼叫 `unregisterCurrentBackgroundItem` 、 `stop`或為止 `reset` 。

   * `unregisterCurrentBackgroundItem` 將背景項目設為nil，並停止擷取和剖析背景資訊清單。

* **PTMetadata.PTBlackoutMetadata** `PTMetadata` A類別，專用於封鎖。

   這可讓您在TVSDK上設定不可見的範圍( `CMTimeRanges`陣列)。 TVSDK會在使用者每次搜尋時檢查這些範圍。 如果已設定，且使用者搜尋至不可見的範圍，TVSDK會強制檢視器到達不可見的範圍結尾。

* **從這裡開始****下一個PTAdMetadata** 通過設定為YES或NO來啟用或禁用即時流 `enableLivePreroll` 上的前滾。 若為否，TVSDK在內容播放前不會明確呼叫前段廣告廣告伺服器，因此不會播放前段廣告。 這對中間輥沒有影響。 預設值為YES。

* **NSNoftigies**

   * `PTTimedMetadataChangedInBackgroundNotification` -當TVSDK偵測到背景資訊清單中已訂閱的標籤，並準備新 `PTTimedMetadata` 的例項時發佈。 通知的物件是目前 `PTMediaPlayerItem` 正在播放的例項。 您可以使用 `PTTimedMetadata` 金鑰從通知的字典 `userInfo` 擷取例 `PTTimedMetadataKey` 項。

   * `PTBackgroundManifestErrorNotification` -當媒體播放器完全無法載入背景資訊清單時發佈，即所有串流URL都會傳回錯誤或無效回應。 通知的物件是目前 `PTMediaPlayerItem` 正在播放的例項。

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * 程式碼：204000
      * 類型：警告
      * 背景資訊清單下載時發生錯誤。
   * `INVALID_SEEK_WARNING` 在不可查找範圍（在中設定）中嘗試查找時 `nonSeekableRanges` 發送 `PTBlackoutMetadata`的。