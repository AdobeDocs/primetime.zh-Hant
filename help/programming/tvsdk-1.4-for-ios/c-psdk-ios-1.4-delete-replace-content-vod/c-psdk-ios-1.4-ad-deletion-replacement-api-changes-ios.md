---
description: 下列TVSDK變更支援廣告刪除和取代。
title: 廣告刪除和取代API變更
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# 廣告刪除和取代API變更{#ad-deletion-and-replacement-api-changes}

下列TVSDK變更支援廣告刪除和取代。

**新API**

* `PTTimeRangeCollection` 是一個公用類別，定義了一組預先定義的範圍和型別：

   * `property PTTimeRangeCollectionType type` 表示時間範圍的型別。
   * `property NSArray* ranges` 用於設定時間範圍。

      陣列中預期的物件型別為 `PTReplacementTimeRange` 或 `CMTimeRange`.

      >[!TIP]
      >
      >陣列的所有物件都必須是相同的型別。

   * `PTTimeRangeCollectionType` 是列舉，定義中定義之範圍的行為。 `PTTimeRangeCollection`：

      * `PTTimeRangeCollectionTypeMarkRanges`：範圍的型別為 *標籤*. 範圍是用來將內容中的範圍標示為廣告。

      * `PTTimeRangeCollectionTypeDeleteRanges`：範圍的型別是「刪除」。 定義的範圍會在廣告插入前從主要內容中移除。
      * `PTTimeRangeCollectionTypeReplaceRanges`：範圍的型別是「取代」。 定義的範圍會從主要以Ads （廣告訊號模式設定為）取代 `PTAdSignalingModeCustomTimeRanges`)。

* `PTReplacementTimeRange`  — 新的公用類別，定義 `PTTimeRangeCollection`：

   * `property CMTimeRange range`  — 定義範圍的開始和持續時間。
   * `property long replacementDuration`  — 如果 `TimeRangeCollection` 是 `PTTimeRangeCollectionTypeReplaceRanges`，則 `replacementDuration` 用於建立投放機會（廣告插入），其持續時間為 `replacementDuration`. 如果 `replacementDuration` 未設定，廣告伺服器將會決定該刊登機會的廣告持續時間和數量。

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges`  — 新增新型別 `PTAdSignalingMode`. 此模式會與 `PTTimeRangeCollection` 具有型別 `PTTimeRangeCollectionReplace` 用於根據取代範圍插入廣告。

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection`  — 用於設定播放內容中標籤/刪除/取代範圍所使用的時間範圍。

* 警告記錄：

   * `UNDEFINED_TIME_RANGES`

      * 型別 — 警告
      * 說明 — 廣告訊號模式定義為自訂範圍，但未定義自訂範圍。
   * `INVALID_TIME_RANGES`

      * 型別 — 警告
      * 說明 — 一或多個時間範圍無效，將被忽略或修改。


**過時的API**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges`  — 此屬性先前用於定義要標示的C3範圍。 現已棄用，因為這些範圍是透過以下方式設定： `PTTimeRangeCollection`.

