---
description: 自定義廣告標籤允許您將一組表示時間線段的TimeRange規範傳遞給TVSDK。
title: TimeRange類
exl-id: 7451c4f6-40df-48b2-a2c7-6d7826724716
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# TimeRange類{#timerange-class}

自定義廣告標籤允許您將一組表示時間線段的TimeRange規範傳遞給TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

集中的每個TimeRange規範都表示播放時間線上由TVSDK內部維護的段，且必須將其適當標籤為與廣告相關的時段。

的 `TimeRange` 類是一個簡單的資料結構，它顯示時間線上的起始位置和結束位置。 這兩個只讀屬性抽象了回放時間軸中時間範圍的概念。

>[!TIP]
>
>這兩個值以毫秒為單位表示。

下面是 `TimeRange` 類：

```java
public final class TimeRange {
    // the start/end values are provided at construction time
    public static TimeRange createRange(long begin, long duration) {...} 

    // only getters are available
    public long getBegin() {...} 
    public long getEnd() {...} 
    public long getDuration() {...}
}
```
