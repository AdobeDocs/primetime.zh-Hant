---
description: TVSDK支援程式化刪除和取代VOD串流中的廣告內容。
title: 廣告刪除和取代API變更
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# 廣告刪除和取代API變更{#ad-deletion-and-replacement-api-changes}

TVSDK支援程式化刪除和取代VOD串流中的廣告內容。

刪除和取代功能可延伸自訂廣告標籤功能。 自訂廣告標籤會將主要內容的區段標示為廣告相關內容句點。 除了標籤這些時間範圍外，您也可以刪除和取代時間範圍。

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

TVSDK的下列變更支援及刪除和取代。

**新API**

* `PTTimeRangeCollection` 是一個公共類，它定義一組預定義的範圍和類型：

   * `property PTTimeRangeCollectionType type` 表示時間範圍的類型。
   * `property NSArray* ranges` 用於設定時間範圍。

      陣列中預期的對象類型為`PTReplacementTimeRange`或`CMTimeRange`。

      >[!TIP]
      >
      >陣列的所有對象都必須是相同的類型。

   * `PTTimeRangeCollectionType` 是enum，用於定義以下定義範圍的行為： `PTTimeRangeCollection`

      * `PTTimeRangeCollectionTypeMarkRanges`:範圍類型為「標 *記」*。這些範圍會用來將內容中的範圍標示為「廣告」。

      * `PTTimeRangeCollectionTypeDeleteRanges`:範圍的類型為「刪除」。在廣告插入前，會從主要內容移除定義的範圍。
      * `PTTimeRangeCollectionTypeReplaceRanges`:範圍的類型為「取代」。定義的範圍從主窗口以Ads（Ad信令模式設定為`PTAdSignalingModeCustomTimeRanges`）替換。

* `PTReplacementTimeRange` -定義以下單一範圍的新公共類 `PTTimeRangeCollection`:

   * `property CMTimeRange range` -定義範圍的開始和持續時間。
   * `property long replacementDuration` -如果類型為 `TimeRangeCollection` , `PTTimeRangeCollectionTypeReplaceRanges`則 `replacementDuration` 用於建立持續時間為的位置機會（廣告插入） `replacementDuration`。如果未設定`replacementDuration`，廣告伺服器將確定該位置機會的廣告持續時間和數量。

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` -新增新類型 `PTAdSignalingMode`。此模式與`PTTimeRangeCollection`搭配使用，類型為`PTTimeRangeCollectionReplace`，以根據取代範圍進行廣告插入。

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` -用於設定回放內容中標籤／刪除／替換範圍中使用的時間範圍。

* 警告記錄檔：

   * `UNDEFINED_TIME_RANGES`

      * 類型——警告
      * 說明——廣告信令模式定義為自訂範圍，但未定義自訂範圍。
   * `INVALID_TIME_RANGES`

      * 類型——警告
      * 說明——一個或多個時間範圍無效，將被忽略或修改。


**已過時的API**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` -此屬性先前用來定義C3範圍以進行標籤。現在已不再提倡，因為這些範圍是透過`PTTimeRangeCollection`設定。