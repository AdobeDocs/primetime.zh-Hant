---
description: ReplaceTimeRange實用程式類是TimeRange類的擴展，將與CustomRangeMetadata一起使用。
seo-description: ReplaceTimeRange實用程式類是TimeRange類的擴展，將與CustomRangeMetadata一起使用。
seo-title: ReplaceTimeRange類
title: ReplaceTimeRange類
uuid: 19c49b26-5096-4429-b30b-bdd2502e3036
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# ReplaceTimeRange類 {#replacetimerange-class}

ReplaceTimeRange實用程式類是TimeRange類的擴展，將與CustomRangeMetadata一起使用。

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

