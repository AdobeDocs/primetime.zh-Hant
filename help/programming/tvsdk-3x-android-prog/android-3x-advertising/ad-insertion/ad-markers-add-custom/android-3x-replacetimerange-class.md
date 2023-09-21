---
description: ReplaceTimeRange公用程式類別是搭配CustomRangeMetadata使用的TimeRange類別的延伸。
title: ReplaceTimeRange類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 0%

---

# ReplaceTimeRange類別 {#replacetimerange-class}

ReplaceTimeRange公用程式類別是搭配CustomRangeMetadata使用的TimeRange類別的延伸。

```java
public class ReplaceTimeRange extends TimeRange {
    // Default constructor method
    public ReplaceTimeRange() { 
        ... 
    }

    // Details of begining, duration and replaceDuration 
    // provided at construction time 
    public ReplaceTimeRange(long begin, long duration, long replaceDuration) { 
        ... 
    }

    // Replace duration
    public long getReplaceDuration() { 
        ... 
    }
}
```
