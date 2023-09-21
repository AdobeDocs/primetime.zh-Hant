---
description: 瀏覽器TVSDK目前支援播放資訊清單和片段不含擴充功能的資料流。
title: 無擴充功能串流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 無擴充功能串流{#extensionless-streams}

瀏覽器TVSDK目前支援播放資訊清單和片段不含擴充功能的資料流。

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

如果 `resourceType` 未提供，UI Framework會從資源URL副檔名中判斷資源型別，然後將其傳遞至 `replaceCurrentResource` 方法。

>[!TIP]
>
>對於無擴充功能資訊清單，請確定 `resourceType` 在UI Framework中載入資源時一律會傳遞。
