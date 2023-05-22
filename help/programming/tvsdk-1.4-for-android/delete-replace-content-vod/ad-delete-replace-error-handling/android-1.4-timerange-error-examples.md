---
description: TVSDK通過合併或替換適當的時間範圍來響應錯誤的時間範圍規範。
title: 時間範圍錯誤示例
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 時間範圍錯誤示例{#time-range-error-examples}

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

