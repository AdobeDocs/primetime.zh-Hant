---
description: TVSDK會根據特定問題處理時間範圍錯誤，例如合併或重新排序不正確定義的時間範圍。
title: 廣告刪除和取代錯誤處理
exl-id: 3147d446-68a1-4e4b-9a29-f464b936d650
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 廣告刪除和取代錯誤處理{#ad-deletion-and-replacement-error-handling}

TVSDK會根據特定問題處理時間範圍錯誤，例如合併或重新排序不正確定義的時間範圍。

TVSDK交易 `timeRanges` 執行預設合併和重新排序時發生錯誤。 首先，它會依據以下專案來排序客戶定義的時間範圍： *開始* 時間。 然後它會根據此排序順序合併相鄰的範圍，並在範圍之間有子集和交集時聯結它們。

TVSDK會依照以下方式處理時間範圍錯誤：

* 順序錯誤 — TVSDK會重新排序時間範圍。
* 子集 — TVSDK會合併時間範圍子集。
* 相交 — TVSDK會合併相交的時間範圍。
* 取代範圍衝突 — TVSDK會從最早出現的位置選擇取代持續時間 `timeRange` 在衝突群組中。

TVSDK會依照下列方式處理與廣告中繼資料的信令模式衝突：

* 如果廣告訊號模式與時間範圍中繼資料衝突，則時間範圍中繼資料一律有優先權。 例如，如果廣告訊號模式設定為伺服器對應或資訊清單提示，且廣告中繼資料中還有MARK時間範圍，則產生的行為是標籤這些範圍，並且不會插入任何廣告。
* 對於REPLACE範圍，如果訊號模式設定為伺服器對應或資訊清單提示，則會按照REPLACE範圍中指定的方式取代範圍，而且不會透過伺服器對應或資訊清單提示插入廣告。 另請參閱 [廣告訊號模式](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

當伺服器未傳回有效值 `AdBreaks`：

* TVSDK會產生並處理 `NOPTimelineOperation` （空白） `AdBreak`. 無廣告播放。

對於具有即時資料流的時間範圍：

* 雖然此C3廣告刪除/取代功能僅針對VOD提供支援，但若在廣告中繼資料中指定，也會為即時資料流處理時間範圍。

## 時間範圍錯誤範例 {#time-range-error-examples}

TVSDK會適當地合併或取代時間範圍，以回應錯誤的時間範圍規格。

在以下範例中，定義了四個相交DELETE時間範圍。 TVSDK會將四個時間範圍合併為一個，因此實際刪除範圍是從0到50秒。

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

在以下範例中，四個REPLACE時間範圍定義為有衝突的時間範圍。 在此情況下，TVSDK會以25s廣告取代0-50s。 它會隨著排序順序中的第一個取代持續時間而改變，因為後續範圍有衝突。

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
