---
description: TVSDK根據特定問題處理時間範圍錯誤，合併或重新排序未正確定義的時間範圍。
title: 廣告刪除和替換錯誤處理
exl-id: 3147d446-68a1-4e4b-9a29-f464b936d650
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 廣告刪除和替換錯誤處理{#ad-deletion-and-replacement-error-handling}

TVSDK根據特定問題處理時間範圍錯誤，合併或重新排序未正確定義的時間範圍。

TVSDK處理 `timeRanges` 執行預設合併和重新排序時出錯。 首先，它按 *開始* 時間。 根據此排序順序，它合併相鄰範圍，並在範圍之間存在子集和交叉點時將其連接。

TVSDK按如下方式處理時間範圍錯誤：

* 無序 — TVSDK重新排序時間範圍。
* 子集 — TVSDK合併時間範圍子集。
* 交叉 — TVSDK合併交叉時間範圍。
* 替換範圍衝突 — TVSDK從最早出現時選擇替換持續時間 `timeRange` 在衝突組中。

TVSDK處理與ad元資料的信令模式衝突，如下所示：

* 如果廣告信令模式與時間範圍元資料衝突，則時間範圍元資料始終具有優先順序。 例如，如果廣告信令模式被設定為伺服器映射或清單提示，並且廣告元資料中還有MARK時間範圍，則產生的行為是標籤範圍，並且不插入廣告。
* 對於REPLACE範圍，如果信令模式設定為伺服器映射或清單提示，則按照REPLACE範圍中指定的方式替換該範圍，並且不會通過伺服器映射或清單提示插入廣告。 請參閱 [廣告信令模式](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md)。

當伺服器未返回有效時 `AdBreaks`:

* TVSDK生成並處理 `NOPTimelineOperation` 為空 `AdBreak`。 沒有廣告。

對於具有即時流的時間範圍：

* 儘管此C3和刪除/替換功能僅用於VOD，但如果在ad元資料中指定，則會處理即時流的時間範圍。

## 時間範圍錯誤示例 {#time-range-error-examples}

TVSDK通過合併或替換適當的時間範圍來響應錯誤的時間範圍規範。

在以下示例中，定義了四個相交的DELETE時間範圍。 TVSDK將四個時間範圍合併為一個，因此實際刪除範圍是0到50s。

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

在下例中，四個REPLACE時間範圍定義為衝突的時間範圍。 在這種情況下，TVSDK用25個廣告代替0到50個。 它與排序順序中的第一個替換持續時間相同，因為後續範圍記憶體在衝突。

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
