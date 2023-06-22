---
description: 瀏覽器TVSDK目前支援播放資訊清單和片段不包含擴充功能的資料流。
title: 無擴充功能資料流
exl-id: ef81bfd2-2bfa-4ff7-b826-fd80802b3c07
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 無擴充功能資料流{#extensionless-streams}

瀏覽器TVSDK目前支援播放資訊清單和片段不包含擴充功能的資料流。

## 片段層級 {#section_0E035129501D4A77BBC14192D8A53A86}

瀏覽器TVSDK會剖析回應的前幾個位元組，以偵測無擴充功能片段的內容型別。 如果未偵測到有效的內容型別，瀏覽器TVSDK會擲回錯誤。

## 資訊清單層級 {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

瀏覽器TVSDK使用 `mediaResource.resourceType` 傳入的引數 `replaceCurrentResource` 偵測資訊清單URL內容型別的方法。 如需詳細資訊，請參閱 `AdobePSDK.MediaPlayer` 類別。

在UI Framework播放器中，您可以在媒體資源中指定資源型別，如下所示：

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

若 `resourceType` ui Framework會從資源URL副檔名中判斷資源型別，然後將其傳遞至 `replaceCurrentResource` 方法。

>[!TIP]
>
>對於無擴充功能的資訊清單，請確定 `resourceType` 在UI Framework中載入資源時一律會傳遞。
