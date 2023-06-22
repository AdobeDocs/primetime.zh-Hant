---
description: TimeRangeCollection公用程式類別會擷取TimeRange規格的有序集合的概念，並提供將自身轉譯為Metadata例項的服務。
title: TimeRangeCollection類別
exl-id: 2e5160b0-2254-4a40-8c32-fe3e05b9fc30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---

# TimeRangeCollection類別{#timerangecollection-class}

TimeRangeCollection公用程式類別會擷取TimeRange規格的有序集合的概念，並提供將自身轉譯為Metadata例項的服務。

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

集合型別的已定義值為 `MARK_RANGES`， `DELETE_RANGES`、和 `REPLACE_RANGES`. 您可以建立 `TimeRangeCollection`使用這三種型別。
