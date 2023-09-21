---
description: TimeRangeCollection公用程式類別會擷取TimeRange規格的有序集合概念，並提供將自身轉譯為Metadata執行個體的服務。
title: TimeRangeCollection類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---

# TimeRangeCollection類別{#timerangecollection-class}

TimeRangeCollection公用程式類別會擷取TimeRange規格的有序集合概念，並提供將自身轉譯為Metadata執行個體的服務。

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

集合型別的已定義值為 `MARK_RANGES`， `DELETE_RANGES`、和 `REPLACE_RANGES`. 您可以建立 `TimeRangeCollection`s使用這三種型別。
