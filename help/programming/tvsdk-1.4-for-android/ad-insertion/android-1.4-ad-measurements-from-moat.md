---
description: TVSDK會從FreeWheel和其他提供VAST回應的廣告伺服器取得資訊。 FreeWheel在VAST響應中提供來自Moat服務的資訊。 Moat服務會以更準確的方式計算廣告曝光數，以更準確地顯示創意人員是否擷取或忽略觀眾的興趣。
seo-description: TVSDK會從FreeWheel和其他提供VAST回應的廣告伺服器取得資訊。 FreeWheel在VAST響應中提供來自Moat服務的資訊。 Moat服務會以更準確的方式計算廣告曝光數，以更準確地顯示創意人員是否擷取或忽略觀眾的興趣。
seo-title: 來自Moat的廣告度量
title: 來自Moat的廣告度量
uuid: 73ef3a14-7ad6-4e67-8ad3-eabbeb898a09
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 來自Moat的廣告度量{#ad-measurements-from-moat}

TVSDK會從FreeWheel和其他提供VAST回應的廣告伺服器取得資訊。 FreeWheel在VAST響應中提供來自Moat服務的資訊。 Moat服務會以更準確的方式計算廣告曝光數，以更準確地顯示創意人員是否擷取或忽略觀眾的興趣。

Moat是一項服務，可測量從瀏覽器到應用程式的多種用途的檢視。 Moat會即時產生跨多個平台的行銷分析資料。

VAST回應XML包含您的程式碼可讀取的屬性和元素、最外層 `Ad id` 屬性和最外層 `Extension` 元素。 不論如何，您的程式碼都可使用TVSDK來儲存資 `Ad id` 訊和資 `Extension` 訊，然後以樹狀結構組織資訊。 透過此組織，您的程式碼可以從任何層級擷取資料，並將資料傳遞至所需的任何位置。 最外緣屬性的值可 `Ad id` 讓您的程式碼協調關聯促銷活動的資訊。

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

Freewheel也可以在元素 `id` 中設定屬 `Ad` 性，如下例所示。

```xml
<Ad id="118566" sequence="1">
```

請參閱類別的API檔案 `NetworkAdInfo`。
