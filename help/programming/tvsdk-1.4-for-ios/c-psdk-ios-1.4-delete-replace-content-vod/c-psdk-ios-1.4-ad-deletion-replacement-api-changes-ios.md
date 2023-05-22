---
description: TVSDK中的以下更改支援刪除和替換。
title: 廣告刪除和替換API更改
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# 廣告刪除和替換API更改{#ad-deletion-and-replacement-api-changes}

TVSDK中的以下更改支援刪除和替換。

**新API**

* `PTTimeRangeCollection` 是定義預定義的一組範圍和類型的公共類：

   * `property PTTimeRangeCollectionType type` 指示時間範圍的類型。
   * `property NSArray* ranges` 用於設定時間範圍。

      陣列中預期的對象類型為 `PTReplacementTimeRange` 或 `CMTimeRange`。

      >[!TIP]
      >
      >陣列的所有對象必須是同一類型。

   * `PTTimeRangeCollectionType` 是定義在 `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`:範圍的類型為 *標籤*。 該範圍用於將內容中的範圍標籤為廣告。

      * `PTTimeRangeCollectionTypeDeleteRanges`:範圍的類型為「刪除」。 在廣告插入之前，從主內容中刪除所定義的範圍。
      * `PTTimeRangeCollectionTypeReplaceRanges`:範圍的類型為「替換」。 定義的範圍從主端用Ads替換(Ad信令模式設定為 `PTAdSignalingModeCustomTimeRanges`)。

* `PTReplacementTimeRange`  — 新的公共類，定義 `PTTimeRangeCollection`:

   * `property CMTimeRange range`  — 定義範圍的開始和持續時間。
   * `property long replacementDuration`  — 如果 `TimeRangeCollection` 是 `PTTimeRangeCollectionTypeReplaceRanges`，也請參見Wiki頁。 `replacementDuration` 用於建立持續時間為 `replacementDuration`。 如果 `replacementDuration` 未設定，則廣告伺服器將確定該投放機會的廣告持續時間和數量。

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges`  — 已添加新類型 `PTAdSignalingMode`。 此模式與 `PTTimeRangeCollection` 類型 `PTTimeRangeCollectionReplace` 根據替換範圍插入廣告。

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection`  — 用於設定回放內容中標籤/刪除/替換範圍中使用的時間範圍。

* 警告日誌：

   * `UNDEFINED_TIME_RANGES`

      * 類型 — 警告
      * 說明 — 廣告信令模式定義為自定義範圍，但未定義自定義範圍。
   * `INVALID_TIME_RANGES`

      * 類型 — 警告
      * 說明 — 一個或多個時間範圍無效，將忽略或修改。


**棄用的API**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges`  — 此屬性以前用於定義C3範圍以進行標籤。 現在已棄用，因為這些範圍是通過 `PTTimeRangeCollection`。

