---
description: TVSDK會從FreeWheel和其他提供VAST回應的廣告伺服器擷取資訊。 FreeWheel在VAST回應中提供來自Moat服務的資訊。 Moat服務會將廣告曝光次數計入精確度，藉此更能顯示廣告創意是否捕捉或略過觀眾的興趣。
title: 來自Moat的廣告測量
exl-id: c480f152-c09c-49fe-a8fb-d199bbfb0393
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# 來自Moat的廣告測量 {#ad-measurements-from-moat}

TVSDK會從FreeWheel和其他提供VAST回應的廣告伺服器擷取資訊。 FreeWheel在VAST回應中提供來自Moat服務的資訊。 Moat服務會將廣告曝光次數計入精確度，藉此更能顯示廣告創意是否捕捉或略過觀眾的興趣。

Moat是一項測量廣告檢視的服務，涵蓋從瀏覽器到應用程式內部的各種用途。 Moat可跨多個平台即時產生行銷分析資料。

VAST回應XML具有您程式碼可讀取的屬性和元素（最外層） `Ad id` 屬性和最外層 `Extension` 元素。 無論如何，您的程式碼都可以使用TVSDK來儲存 `Ad id` 資訊和 `Extension` 資訊，然後以樹狀結構組織資訊。 有了這個組織，您的程式碼就能從任何層級擷取資料，然後將其傳送至任何需要的位置。 最外層的值 `Ad id` 屬性可讓您的程式碼協調來自相關行銷活動的資訊。

例如，FreeWheel可傳回Extensions元素中的資料。 以下是範例元素。

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

Freewheel也可以設定 `id` 中的屬性 `Ad` 元素，如下面的範例所示。

```xml
<Ad id="118566" sequence="1">
```

如需API資訊，請參閱此類別的API檔案 `NetworkAdInfo`.
