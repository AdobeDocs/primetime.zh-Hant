---
description: TVSDK從FreeWheel和提供VAST響應的其他廣告伺服器獲取資訊。 FreeWheel在VAST響應中提供Moat服務的資訊。 Moat服務能準確計算廣告印象，更準確地顯示創意是否捕捉或忽視受眾的利益。
title: 莫阿的廣告測量
exl-id: c480f152-c09c-49fe-a8fb-d199bbfb0393
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# 莫阿的廣告測量 {#ad-measurements-from-moat}

TVSDK從FreeWheel和提供VAST響應的其他廣告伺服器獲取資訊。 FreeWheel在VAST響應中提供Moat服務的資訊。 Moat服務能準確計算廣告印象，更準確地顯示創意是否捕捉或忽視受眾的利益。

Moat是一種服務，可測量和查看從瀏覽器到應用程式內的各種用途。 Moat跨多個平台即時生成營銷分析資料。

VAST響應XML具有一個屬性和一個您的代碼可以讀取的元素，最外面 `Ad id` 屬性和最外層 `Extension` 的子菜單。 無論如何，您的代碼都可以使用TVSDK保存 `Ad id` 資訊和 `Extension` 資訊，然後將資訊組織成樹形結構。 使用此組織，您的代碼可以從任何級別提取資料，並將其傳遞到需要的任何位置。 最外面的值 `Ad id` 屬性使您的代碼可以協調關聯市場活動中的資訊。

例如，FreeWheel可以在Extensions元素中返回資料。 下面是示例元素。

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

自由輪也可以 `id` 屬性 `Ad` 元素，如下例所示。

```xml
<Ad id="118566" sequence="1">
```

有關API資訊，請參閱類的API文檔 `NetworkAdInfo`。
