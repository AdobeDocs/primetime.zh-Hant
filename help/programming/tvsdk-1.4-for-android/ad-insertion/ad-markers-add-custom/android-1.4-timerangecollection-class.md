---
description: TimeRangeCollection實用程式類抽象了TimeRange規範的有序集合的概念，並提供了將自身轉換為元資料實例的服務。
title: TimeRangeCollection類
exl-id: 1af41267-c222-43ac-84ca-0bf37b6a59de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# TimeRangeCollection類{#timerangecollection-class}

TimeRangeCollection實用程式類抽象了TimeRange規範的有序集合的概念，並提供了將自身轉換為元資料實例的服務。

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

的 `type` 參數是建構子方法簽名中的第一個位置參數，是 `TimeRangeCollection#Type` 枚舉。 這是 `TimeRangeCollection` 類。 此枚舉當前定義的值是 `MARK_RANGES`。 `DELETE_RANGES`, `REPLACE_RANGES`。 您可以建立 `TimeRangeCollection` 對象。
