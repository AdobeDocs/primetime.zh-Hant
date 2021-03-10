---
description: 您可以處理即時視訊串流中的封鎖期，並在封鎖期間提供替代內容。
title: 封鎖API元素
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# 封鎖API元素{#blackout-api-elements}

您可以處理即時視訊串流中的封鎖期，並在封鎖期間提供替代內容。

在即時串流中發生封鎖時，您的播放器會使用事件處理常式來偵測封鎖，並提供替代內容給不符合主串流觀賞資格的使用者。 您的播放器會偵測封鎖期的開始和結束，從主串流切換播放至替代串流，並在封鎖期結束時切換回主串流。

要處理即時流中的封鎖期，請執行以下操作：

1. 在即時串流資訊清單中訂閱封鎖標籤，以設定您的應用程式以偵測封鎖標籤。

   TVSDK本身並不偵測封鎖標籤；您必須訂閱封鎖標籤，才能在資訊清單檔案剖析期間遇到標籤時收到通知。
1. 為您的播放器已訂閱的標籤建立事件監聽器（在此例中為PLAYBACK和LACOLUTES標籤）。

   當您的播放器在前景（主要內容）或背景（替代內容）串流清單中訂閱（例如封鎖標籤）的標籤時，TVSDK會調度`TimedMetadataEvent`並為`TimedMetadataEvent`建立`TimedMetadataObject`。

1. 為前景和背景串流的計時中繼資料事件實施處理常式。

   在這些處理常式中，從計時中繼資料事件物件取得封鎖期的開始和結束時間。
1. 建立在封鎖期開始和結束時切換內容的方法。

   當封鎖期開始時，將主要內容切換至背景，並將替代內容切換為主串流。 繼續擷取並剖析背景中的原始資訊清單，並持續檢查「封鎖結束」標籤，如此當封鎖結束時，播放器就可重新加入原始串流。
1. 如果封鎖期範圍在播放串流的DVR中，請更新不可查看的範圍。

   準備並更新封鎖期不可查找的範圍，以追蹤並處理背景串流上的`TimedMetadata`。

TVSDK提供在實作封鎖期（包括方法、中繼資料和通知）時有用的API元素。

在您的播放器中實施封鎖期解決方案時，可使用下列功能。

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 將當前載入的資源另存為背景資源。如果在此方法之後呼叫`replaceCurrentResource`,TVSDK會繼續下載背景項目的資訊清單，直到您呼叫`unregisterCurrentBackgroundItem`、`release`或`reset`為止。

   * `unregisterCurrentBackgroundItem` 將背景項目設為null，並停止擷取和剖析背景資訊清單。

* **BlackoutMetadata** -

   特定於封鎖的元資料類。

   這可讓您在TVSDK上設定不可檢視的範圍（`TimeRanges`的陣列）。 TVSDK會在使用者每次搜尋時檢查這些範圍。 如果已設定，且使用者搜尋至不可見的範圍，TVSDK會強制檢視器到達不可見的範圍結尾。

* **從這裡開始下** 一個廣告中繼資料透過設定為true或false，啟用或停用即時串 `enableLivePreroll` 流上的前置鏡頭。若為false,TVSDK在內容播放前不會明確呼叫前段廣告的廣告伺服器，因此不會播放前段廣告。 這對中間輥沒有影響。 預設值為true。

* **MediaPlayer.LacoliquesEventListener**

   * `onTimedMetadataInBackgroundItem` -在偵測到背景資訊清單中已訂閱的標籤，並準備新 `TimedMetadata` 的例項時傳送。`TimedMetadata`實例作為參數派發。

   * `onBackgroundManifestFailed` -當媒體播放器完全無法載入背景資訊清單時傳送，即所有串流URL都傳回錯誤或無效回應。

* **通知**

   * `BACKGROUND_MANIFEST_WARNING`

      * 程式碼：204000
      * 類型：警告
      * 背景資訊清單下載時發生錯誤。