---
description: TimeRangeCollection實用程式類抽象了有序集合TimeRange規範的概念，並提供了將自身轉換為元資料實例的服務。
seo-description: TimeRangeCollection實用程式類抽象了有序集合TimeRange規範的概念，並提供了將自身轉換為元資料實例的服務。
seo-title: TimeRangeCollection類
title: TimeRangeCollection類
uuid: 5705dc9d-4325-44b0-b5aa-196d09c3a67e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# TimeRangeCollection類{#timerangecollection-class}

TimeRangeCollection實用程式類抽象了有序集合TimeRange規範的概念，並提供了將自身轉換為元資料實例的服務。

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```java
public final class TimeRangeCollection {
    // default constructor method
    public TimeRangeCollection(Type type) {...}

    // the list of timerange specifications provided at construction time 
    public TimeRangeCollection(Type type, List<TimeRange> timeRanges) {...}

    // timerange specs can also be added later
    public void addTimeRange(TimeRange timeRange) {...}

    // translate the set of timerange specs into a Metadata instance 
    public Metadata toMetadata(Metadata options) {...}
}
```

參 `type` 數是建構函式方法簽名中的第一個位置參數，是列舉的例 `TimeRangeCollection#Type` 項。 這是課程的一 `TimeRangeCollection` 部分。 此枚舉當前定義的值 `MARK_RANGES`為 `DELETE_RANGES`、和 `REPLACE_RANGES`。 您可以使用這 `TimeRangeCollection` 三種類型來建立物件。
