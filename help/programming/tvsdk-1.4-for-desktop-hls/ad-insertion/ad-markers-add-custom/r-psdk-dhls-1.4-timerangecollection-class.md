---
description: TimeRangeCollection實用程式類抽象了有序集合TimeRange規範的概念，並提供了將自身轉換為元資料實例的服務。
title: TimeRangeCollection類
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# TimeRangeCollection類{#timerangecollection-class}

TimeRangeCollection實用程式類抽象了有序集合TimeRange規範的概念，並提供了將自身轉換為元資料實例的服務。

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

系列類型的定義值為`MARK_RANGES`、`DELETE_RANGES`和`REPLACE_RANGES`。 您可以使用這三種類型建立`TimeRangeCollection`。
