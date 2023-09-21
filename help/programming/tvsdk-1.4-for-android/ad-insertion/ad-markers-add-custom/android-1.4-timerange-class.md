---
description: 自訂廣告標籤可讓您將代表時間表區段的一組TimeRange規格傳遞給TVSDK。
title: TimeRange類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# TimeRange類別{#timerange-class}

自訂廣告標籤可讓您將代表時間表區段的一組TimeRange規格傳遞給TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

集合中的每個TimeRange規格都代表播放時間表上的區段，該區段由TVSDK內部維護，且必須適當地標示為廣告相關期間。

此 `TimeRange` class是簡單的資料結構，可在時間軸上顯示開始位置和結束位置。 這兩個唯讀屬性抽象化了播放時間軸中時間範圍的概念。

>[!TIP]
>
>這兩個值都以毫秒為單位表示。

以下為摘要 `TimeRange` 類別：

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
