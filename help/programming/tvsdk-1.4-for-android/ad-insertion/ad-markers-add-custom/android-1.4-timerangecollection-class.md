---
description: TimeRangeCollection實用程式類抽象了有序集合TimeRange規範的概念，並提供了將自身轉換為元資料實例的服務。
title: TimeRangeCollection類
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

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

`type`參數是建構函式方法簽名中的第一個位置參數，是`TimeRangeCollection#Type`列舉的例項。 這是`TimeRangeCollection`類的一部分。 此枚舉當前定義的值為`MARK_RANGES` 、 `DELETE_RANGES`和`REPLACE_RANGES`。 您可以使用這三種類型建立`TimeRangeCollection`對象。
