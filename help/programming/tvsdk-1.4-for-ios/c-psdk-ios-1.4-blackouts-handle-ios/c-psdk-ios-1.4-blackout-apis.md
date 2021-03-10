---
description: TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。
title: 封鎖API元素
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 封鎖API元素{#blackout-api-elements}

TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。

在您的播放器中實施封鎖期解決方案時，可使用下列功能。

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 將當前載入的資源另存為背景資源。如果在此方法後呼叫`replaceCurrentItemWithPlayerItem`,TVSDK會繼續下載背景項目的資訊清單，直到您呼叫`unregisterCurrentBackgroundItem`、`stop`或`reset`為止。

   * `unregisterCurrentBackgroundItem` 將背景項目設為nil，並停止擷取和剖析背景資訊清單。

* **PTMetadata.** PTBlackoutMetadataA類， `PTMetadata` 專用於封鎖期。

   這可讓您在TVSDK上設定不可見的範圍（`CMTimeRanges`的陣列）。 TVSDK會在使用者每次搜尋時檢查這些範圍。 如果已設定，且使用者搜尋至不可見的範圍，TVSDK會強制檢視器到達不可見的範圍結尾。

* **從這裡開** **** 始NEXTPTAdMetadata透過設定為YES或NO，啟用或停用即時串 `enableLivePreroll` 流上的前置播放。若為否，TVSDK在內容播放前不會明確呼叫前段廣告廣告伺服器，因此不會播放前段廣告。 這對中間輥沒有影響。 預設值為YES。

* **NSNoftigies**

   * `PTTimedMetadataChangedInBackgroundNotification` -當TVSDK偵測到背景資訊清單中的訂閱標籤，並準備新 `PTTimedMetadata` 的例項時發佈。通知的對象是當前正在播放的`PTMediaPlayerItem`實例。 您可以使用`PTTimedMetadataKey`鍵從通知的`userInfo`字典中讀取`PTTimedMetadata`實例。

   * `PTBackgroundManifestErrorNotification` -當媒體播放器完全無法載入背景資訊清單時發佈，即所有串流URL都會傳回錯誤或無效回應。通知的對象是當前正在播放的`PTMediaPlayerItem`實例。

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * 程式碼：204000
      * 類型：警告
      * 背景資訊清單下載時發生錯誤。
   * `INVALID_SEEK_WARNING` 在不可查找範圍（在中設定）中嘗試查找時 `nonSeekableRanges` 發送 `PTBlackoutMetadata`的。


