---
description: TVSDK會根據需要合併或取代時間範圍，以回應錯誤的時間範圍規格。
seo-description: TVSDK會根據需要合併或取代時間範圍，以回應錯誤的時間範圍規格。
seo-title: 時間範圍錯誤範例
title: 時間範圍錯誤範例
uuid: 327b38dc-6aa3-49a7-b5e7-c343b704c5c3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 時間範圍錯誤範例{#time-range-error-examples}

TVSDK會根據需要合併或取代時間範圍，以回應錯誤的時間範圍規格。

在以下示例中，定義了四個相交的DELETE時間範圍。 TVSDK將4個時間範圍合併為1，因此實際刪除範圍是0-50秒。

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

