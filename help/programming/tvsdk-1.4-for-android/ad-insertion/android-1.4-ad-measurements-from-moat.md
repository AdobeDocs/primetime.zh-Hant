---
description: TVSDK會從FreeWheel和其他提供VAST回應的廣告伺服器取得資訊。 FreeWheel在VAST響應中提供來自Moat服務的資訊。 Moat服務會以更準確的方式計算廣告曝光數，以更準確地顯示創意人員是否擷取或忽略觀眾的興趣。
title: 來自Moat的廣告度量
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# 來自Moat{#ad-measurements-from-moat}的廣告測量

TVSDK會從FreeWheel和其他提供VAST回應的廣告伺服器取得資訊。 FreeWheel在VAST響應中提供來自Moat服務的資訊。 Moat服務會以更準確的方式計算廣告曝光數，以更準確地顯示創意人員是否擷取或忽略觀眾的興趣。

Moat是一項服務，可測量從瀏覽器到應用程式的多種用途的檢視。 Moat會即時產生跨多個平台的行銷分析資料。

VAST響應XML具有一個屬性和一個您的代碼可以讀取的元素、最外面的`Ad id`屬性和最外面的`Extension`元素。 無論如何，您的程式碼都可以使用TVSDK來儲存`Ad id`資訊和`Extension`資訊，然後以樹狀結構來組織資訊。 透過此組織，您的程式碼可以從任何層級擷取資料，並將資料傳遞至所需的任何位置。 最外緣`Ad id`屬性的值可讓您的程式碼協調相關促銷活動的資訊。

例如，FreeWheel可以傳回「延伸功能」元素中的資料。 以下是範例元素。

```xml
<?xml version="1.0"?> 
<Extensions> 
  <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
      <MeasurementInfo renditionID="6398737" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions> 
```

Freewheel也可以在`Ad`元素中設定`id`屬性，如下例所示。

```xml
<Ad id="118566" sequence="1">
```

請參閱`NetworkAdInfo`類別的API文檔。
