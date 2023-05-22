---
description: TVSDK從FreeWheel和提供VAST響應的其他伺服器獲取資訊。 FreeWheel在VAST響應中提供Moat服務的資訊。 Moat服務能準確計算廣告印象，更準確地顯示創意人士捕捉或忽視觀眾的興趣。
title: 莫阿的廣告測量
exl-id: 6148268c-8b18-4a94-8209-097d0ae6446b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# 莫阿的廣告測量 {#ad-measurements-from-moat}

TVSDK從FreeWheel和提供VAST響應的其他伺服器獲取資訊。 FreeWheel在VAST響應中提供Moat服務的資訊。 Moat服務能準確計算廣告印象，更準確地顯示創意人士捕捉或忽視觀眾的興趣。

Moat是一種服務，可測量和查看從瀏覽器到應用程式內的各種用途。 Moat跨多個平台即時生成營銷分析資料。

VAST響應XML具有一個屬性和一個您的代碼可以讀取的元素、最外面的ad id屬性和最外面的擴展元素。 無論如何，代碼都可以使用TVSDK保存廣告ID資訊和擴展資訊，並以樹結構組織資訊。 使用此組織，您的代碼可以從任何級別提取資料，並將其傳遞到需要的任何位置。 最外面的ad id屬性的值使您的代碼能夠協調來自關聯市場活動的資訊。

例如，FreeWheel可以在Extensions元素中返回資料。 下面是示例元素。

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

Freewheel還可以在Ad元素中設定id屬性，如下例所示。

```
<Ad id="118566" sequence="1">
```

請參閱類的API文檔 `PTNetworkAdInfo` 在 `PTAdAsset`。
