---
description: 自訂廣告標籤可讓您將一組代表時間軸區段的TimeRange規格傳遞至TVSDK。
title: TimeRange類
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# TimeRange類{#timerange-class}

自訂廣告標籤可讓您將一組代表時間軸區段的TimeRange規格傳遞至TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

集合中的每個`TimeRange`規格代表播放時間軸上由TVSDK內部維護且必須適當標示為廣告相關時段的區段。

`TimeRange`類別是簡單的資料結構，可顯示時間軸上的開始位置和結束位置。 這兩個唯讀屬性抽象了播放時間軸中時間範圍的概念。

>[!TIP]
>
>這兩個值都以毫秒錶示。

以下是`TimeRange`類的摘要：

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
