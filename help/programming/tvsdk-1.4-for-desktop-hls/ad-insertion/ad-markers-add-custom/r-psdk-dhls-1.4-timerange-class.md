---
description: 自訂廣告標籤可讓您將代表時間表區段的一組TimeRange規格傳遞給TVSDK。
title: TimeRange類別
exl-id: 9dc2abe1-189a-4ef4-9918-37835014bf1b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# TimeRange類別{#timerange-class}

自訂廣告標籤可讓您將代表時間表區段的一組TimeRange規格傳遞給TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

每個 `TimeRange` 集合中的規格代表TVSDK內部維護之播放時間表上的區段，且必須適當地標示為廣告相關時段。

此 `TimeRange` class是簡單的資料結構，可顯示時間軸上的開始位置和結束位置。 這兩個唯讀屬性抽象化了播放時間軸中時間範圍的概念。

>[!TIP]
>
>這兩個值都以毫秒為單位表示。

以下是TimeRange類別的摘要：

```
public final class TimeRange {
    // the start/end values are provided at construction 
    public static function createRange(begin:Number, duration:Number {…}
 
    public function get begin():Number {…}
    public function get end():Number {…}
    public function get duration():Number {…}
}
```
