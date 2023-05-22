---
description: TVSDK根據特定問題處理時間範圍錯誤，合併或重新排序未正確定義的時間範圍。
title: 廣告刪除和替換錯誤處理
exl-id: 86970989-82e0-4e6f-81fb-beee70870c69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 廣告刪除和替換錯誤處理 {#ad-deletion-and-replacement-error-handling}

TVSDK根據特定問題處理時間範圍錯誤，合併或重新排序未正確定義的時間範圍。

TVSDK處理 `timeRanges` 執行預設合併和重新排序時出錯。 首先，它按 *開始* 時間。 根據此排序順序，它合併相鄰範圍，並在範圍之間存在子集和交叉點時將其連接。

TVSDK按如下方式處理時間範圍錯誤：

* 無序 — TVSDK重新排序時間範圍。
* 子集 — TVSDK合併時間範圍子集。
* 交叉 — TVSDK合併交叉時間範圍。
* 替換範圍衝突 — TVSDK從最早出現時選擇替換持續時間 `timeRange` 在衝突組中。

TVSDK按如下方式處理信令模式衝突：

* 如果定義了REPLACE範圍，TVSDK將自動將信令模式更改為CUSTOM_RANGE。
* 如果定義了DELETE範圍或MARK範圍，且信令模式為CUSTOM_RANGE，則TVSDK會刪除或標籤這些範圍。 在本例中沒有廣告插入。
* 如果DELETE範圍或MARK範圍定義了替換持續時間，則TVSDK將忽略此持續時間。

當伺服器未返回有效時 `AdBreaks`:

* TVSDK生成並處理 `NOPTimelineOperation` 為空 `AdBreak`。 沒有廣告。

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
