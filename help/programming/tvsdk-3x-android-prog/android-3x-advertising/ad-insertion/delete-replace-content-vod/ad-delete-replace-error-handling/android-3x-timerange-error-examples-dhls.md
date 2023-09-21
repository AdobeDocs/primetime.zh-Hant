---
description: TVSDK會適當地合併或取代時間範圍，以回應錯誤的時間範圍規格。
title: 時間範圍錯誤範例
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 時間範圍錯誤範例 {#time-range-error-examples}

TVSDK會適當地合併或取代時間範圍，以回應錯誤的時間範圍規格。

**DELETE時間範圍**

在下列範例中，定義了四個相交DELETE時間範圍。 TVSDK將四個時間範圍合併在一起，因此實際刪除範圍是從0到50秒。

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000
        },
        {
            "begin": 20000,
            "end": 50000
        },
        {
            "begin": 0,
            "end": 30000
        },
        {
            "begin": 30000,
            "end": 40000
        }
    ]
}
```

**取代時間範圍**

在下列範例中，四個REPLACE時間範圍定義為有衝突的時間範圍。 在此案例中，TVSDK以25s廣告取代0至50。 它會隨著排序順序中的第一個取代持續時間而改變，因為後續範圍中會有衝突。

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000,
            "replace-duration": 15000
        },
        {
            "begin": 20000,
            "end": 50000,
            "replace-duration": 20000
        },
        {
            "begin": 0,
            "end": 30000,
            "replace-duration": 25000
        },
        {
            "begin": 30000,
            "end": 40000,
            "replace-duration": 30000
        }
    ]
}
```
