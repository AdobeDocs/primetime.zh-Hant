---
description: 瀏覽器TVSDK當前支援播放清單和片段不包含擴展的流。
title: 無擴展流
exl-id: ef81bfd2-2bfa-4ff7-b826-fd80802b3c07
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 無擴展流{#extensionless-streams}

瀏覽器TVSDK當前支援播放清單和片段不包含擴展的流。

## 碎片級別 {#section_0E035129501D4A77BBC14192D8A53A86}

瀏覽器TVSDK解析響應的前幾個位元組，以檢測無擴展片段的內容類型。 如果未檢測到有效的內容類型，則瀏覽器TVSDK將引發錯誤。

## 清單級別 {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

瀏覽器TVSDK使用 `mediaResource.resourceType` 傳遞的參數 `replaceCurrentResource` 用於檢測清單URL的內容類型的方法。 有關詳細資訊，請參見 `AdobePSDK.MediaPlayer` 類。

在UI Framework播放器中，可以按如下方式指定媒體資源中的資源類型：

```js
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
  player: { 
    mediaResource: { 
      resourceUrl:'Specify Resource Url', 
      resourceType: ‘Specify Resource Type. Refer AdobePSDK.MediaResourceType' 
    } 
  } 
}); 
```

如果 `resourceType` 未提供，UI框架從資源URL擴展確定資源類型，然後將其傳遞給 `replaceCurrentResource` 的雙曲餘切值。

>[!TIP]
>
>對於無擴展清單，請確保 `resourceType` 在UI框架中載入資源時始終傳遞。
