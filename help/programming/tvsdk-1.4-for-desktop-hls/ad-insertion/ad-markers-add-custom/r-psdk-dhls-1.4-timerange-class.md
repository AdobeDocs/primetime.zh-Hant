---
description: 自訂廣告標籤可讓您將一組代表時間軸區段的TimeRange規格傳遞至TVSDK。
seo-description: 自訂廣告標籤可讓您將一組代表時間軸區段的TimeRange規格傳遞至TVSDK。
seo-title: TimeRange類
title: TimeRange類
uuid: 5d0c979e-cc63-4fdd-becc-b0e3987b0891
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# TimeRange類{#timerange-class}

自訂廣告標籤可讓您將一組代表時間軸區段的TimeRange規格傳遞至TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

該集 `TimeRange` 中的每個規格代表播放時間軸上由TVSDK內部維護且必須適當標示為廣告相關時段的區段。

類別 `TimeRange` 是簡單的資料結構，可顯示時間軸上的開始位置和結束位置。 這兩個唯讀屬性抽象了播放時間軸中時間範圍的概念。

>[!TIP]
>
>這兩個值都以毫秒錶示。

以下是TimeRange類的摘要：

```
public final class TimeRange {
    // the start/end values are provided at construction 
    public static function createRange(begin:Number, duration:Number {…}
 
    public function get begin():Number {…}
    public function get end():Number {…}
    public function get duration():Number {…}
}
```

