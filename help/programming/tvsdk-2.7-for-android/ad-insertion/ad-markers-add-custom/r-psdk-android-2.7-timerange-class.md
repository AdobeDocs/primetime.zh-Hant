---
description: 自訂廣告標籤可讓您將一組代表時間軸區段的TimeRange規格傳遞至TVSDK。
seo-description: 自訂廣告標籤可讓您將一組代表時間軸區段的TimeRange規格傳遞至TVSDK。
seo-title: TimeRange類
title: TimeRange類
uuid: e5a176af-29b9-4aa6-848e-5aba7988584b
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# TimeRange類 {#timerange-class}

自訂廣告標籤可讓您將一組代表時間軸區段的TimeRange規格傳遞至TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

該集 `TimeRange` 中的每個規格代表播放時間軸上由TVSDK內部維護且必須適當標示為廣告相關時段的區段。

類別 `TimeRange` 是簡單的資料結構，可顯示時間軸上的開始位置和結束位置。 這兩個唯讀屬性抽象了播放時間軸中時間範圍的概念。

>[!TIP]
>
>這兩個值都以毫秒錶示。

以下是該類的摘 `TimeRange` 要：

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

