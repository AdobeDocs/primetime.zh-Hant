---
description: TimeRangeCollection公用程式類別會擷取TimeRange規格的有序集合概念，並提供將自身轉譯為Metadata執行個體的服務。
title: TimeRangeCollection類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# TimeRangeCollection類別{#timerangecollection-class}

TimeRangeCollection公用程式類別會擷取TimeRange規格的有序集合概念，並提供將自身轉譯為Metadata執行個體的服務。

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

此 `type` 引數，是建構函式方法的簽章中的第一個位置引數，是 `TimeRangeCollection#Type` 分項清單。 這是 `TimeRangeCollection` 類別。 此列舉目前定義的值為 `MARK_RANGES`， `DELETE_RANGES`、和 `REPLACE_RANGES`. 您可以建立 `TimeRangeCollection` 物件。
