---
description: 自定義廣告標籤允許您將一組表示時間線段的TimeRange規範傳遞給TVSDK。
title: TimeRange類
exl-id: 9dc2abe1-189a-4ef4-9918-37835014bf1b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# TimeRange類{#timerange-class}

自定義廣告標籤允許您將一組表示時間線段的TimeRange規範傳遞給TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

每個 `TimeRange` 集合中的規範表示播放時間線上由TVSDK內部維護的段，且必須適當地標籤為與廣告相關的時段。

的 `TimeRange` 類是一個簡單的資料結構，它顯示時間線上的起始位置和結束位置。 這兩個只讀屬性抽象了回放時間軸中時間範圍的概念。

>[!TIP]
>
>這兩個值以毫秒為單位表示。

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
