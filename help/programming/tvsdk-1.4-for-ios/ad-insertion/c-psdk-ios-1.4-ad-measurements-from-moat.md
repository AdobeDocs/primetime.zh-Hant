---
description: TVSDK會從FreeWheel和其他提供VAST回應的伺服器取得資訊。 FreeWheel在VAST響應中提供來自Moat服務的資訊。 Moat服務以更準確的方式計算廣告曝光數，更能顯示創意人員捕捉或忽略觀眾的興趣。
seo-description: TVSDK會從FreeWheel和其他提供VAST回應的伺服器取得資訊。 FreeWheel在VAST響應中提供來自Moat服務的資訊。 Moat服務以更準確的方式計算廣告曝光數，更能顯示創意人員捕捉或忽略觀眾的興趣。
seo-title: 來自Moat的廣告度量
title: 來自Moat的廣告度量
uuid: 76fa9ca0-58bd-44fe-82ce-72fdf6fcc28c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 來自Moat{#ad-measurements-from-moat}的廣告測量

TVSDK會從FreeWheel和其他提供VAST回應的伺服器取得資訊。 FreeWheel在VAST響應中提供來自Moat服務的資訊。 Moat服務以更準確的方式計算廣告曝光數，更能顯示創意人員捕捉或忽略觀眾的興趣。

Moat是一項服務，可測量從瀏覽器到應用程式的多種用途的檢視。 Moat會即時產生跨多個平台的行銷分析資料。

VAST回應XML包含您的程式碼可讀取的屬性和元素、最外層的廣告id屬性和最外層的延伸元素。 不論如何，您的程式碼都可使用TVSDK來儲存廣告ID資訊和擴充功能資訊，並以樹狀結構組織資訊。 透過此組織，您的程式碼可以從任何層級擷取資料，並將資料傳遞至所需的任何位置。 最外緣廣告id屬性的值可讓您的程式碼協調關聯促銷活動的資訊。

例如，FreeWheel可以傳回「延伸功能」元素中的資料。 以下是範例元素。

```xml
<Extensions> 
   <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
     <MeasurementInfo renditionID="6398737" type="MediaFile"> 
      <MoatID> 
       <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
       <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID> 
        <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
        <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions>
```

Freewheel也可以在Ad元素中設定id屬性，如下例所示。

```
<Ad id="118566" sequence="1">
```

請參閱`PTAdAsset`中`PTNetworkAdInfo`類別的API文檔。
