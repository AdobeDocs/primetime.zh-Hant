---
description: TVSDK會根據特定問題處理時間範圍錯誤，或合併或重新排序未正確定義的時間範圍。
title: 廣告刪除和取代錯誤處理
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# 廣告刪除和替換錯誤處理{#ad-deletion-and-replacement-error-handling}

TVSDK會根據特定問題處理時間範圍錯誤，或合併或重新排序未正確定義的時間範圍。

TVSDK會執行預設合併和重新排序，處理`timeRanges`錯誤。 首先，它會依&#x200B;*begin*&#x200B;時間對客戶定義的時間範圍進行排序。 根據這種排序順序，它然後合併相鄰範圍，如果範圍之間有子集和交集，則將其連接。

TVSDK可處理下列時間範圍錯誤：

* 順序錯誤- TVSDK會重新排序時間範圍。
* 子集- TVSDK合併時間範圍子集。
* 交集- TVSDK會合併相交的時間範圍。
* 取代範圍衝突- TVSDK會從衝突群組中最早出現的`timeRange`選擇取代持續時間。

TVSDK可處理與廣告中繼資料的訊號模式衝突，如下所示：

* 如果廣告信令模式與時間範圍元資料衝突，則時間範圍元資料始終具有優先順序。 例如，如果廣告信令模式被設為伺服器地圖或資訊清單提示，而廣告中繼資料中也有MARK時間範圍，則產生的行為是已標籤範圍，且未插入廣告。
* 對於REPLACE範圍，如果信令模式被設定為伺服器映射或資訊清單提示，則該範圍將按照REPLACE範圍中指定的方式被替換，並且不會通過伺服器映射或資訊清單提示插入廣告。 請參閱[廣告信令模式](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md)。

當伺服器未返回有效的`AdBreaks`時：

* TVSDK會針對空的`AdBreak`產生並處理`NOPTimelineOperation`。 沒有廣告播放。

對於具有即時串流的時間範圍：

* 雖然此C3廣告刪除／取代功能僅針對VOD提供支援，但即時串流的時間範圍也會在廣告中繼資料中指定時處理。

## 時間範圍錯誤示例{#time-range-error-examples}

TVSDK會根據需要合併或取代時間範圍，以回應錯誤的時間範圍規格。

在下例中，定義了四個相交的DELETE時間範圍。 TVSDK將4個時間範圍合併為1，因此實際刪除範圍是0-50秒。

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000
    }, {
        "begin": 20000,
        "end": 50000
    }, {
        "begin": 0,
        "end": 30000
    }, {
        "begin": 30000,
        "end": 40000
    } ]
}
```

在以下示例中，四個REPLACE時間範圍定義為衝突的時間範圍。 在此例中，TVSDK會以25個廣告取代0-50。 它會依排序順序排列第一個取代期間，因為後續範圍中會有衝突。

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000,
        "replace-duration": 15000
    }, {
        "begin": 20000,
        "end": 50000,
        "replace-duration": 20000
    }, {
        "begin": 0,
        "end": 30000,
        "replace-duration": 25000
    }, {
        "begin": 30000,
        "end": 40000,
        "replace-duration": 30000
    } ]
}
```
