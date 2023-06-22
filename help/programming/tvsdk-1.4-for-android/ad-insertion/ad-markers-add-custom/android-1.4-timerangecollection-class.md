---
description: TimeRangeCollection公用程式類別會擷取TimeRange規格的有序集合的概念，並提供將自身轉譯為Metadata例項的服務。
title: TimeRangeCollection類別
exl-id: 1af41267-c222-43ac-84ca-0bf37b6a59de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# TimeRangeCollection類別{#timerangecollection-class}

TimeRangeCollection公用程式類別會擷取TimeRange規格的有序集合的概念，並提供將自身轉譯為Metadata例項的服務。

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

此 `type` parameter是建構函式方法的簽章中的第一個位置引數，是 `TimeRangeCollection#Type` 分項清單。 這是 `TimeRangeCollection` 類別。 目前由此分項清單定義的值為 `MARK_RANGES`， `DELETE_RANGES`、和 `REPLACE_RANGES`. 您可以建立 `TimeRangeCollection` 物件。
