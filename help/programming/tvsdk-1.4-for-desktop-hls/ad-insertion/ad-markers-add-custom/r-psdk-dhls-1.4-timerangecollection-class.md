---
description: TimeRangeCollection實用程式類抽象了有序集合TimeRange規範的概念，並提供了將自身轉換為元資料實例的服務。
seo-description: TimeRangeCollection實用程式類抽象了有序集合TimeRange規範的概念，並提供了將自身轉換為元資料實例的服務。
seo-title: TimeRangeCollection類
title: TimeRangeCollection類
uuid: da781df4-6b19-47e1-8dc5-ea83c139f061
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

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

系列類型的定義值 `MARK_RANGES`為 `DELETE_RANGES`、和 `REPLACE_RANGES`。 您可以使 `TimeRangeCollection`用這三種類型建立。
