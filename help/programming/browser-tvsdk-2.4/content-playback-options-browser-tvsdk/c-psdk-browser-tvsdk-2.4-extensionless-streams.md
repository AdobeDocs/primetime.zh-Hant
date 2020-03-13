---
description: 瀏覽器TVSDK目前支援播放清單和片段不含擴充功能的串流。
seo-description: 瀏覽器TVSDK目前支援播放清單和片段不含擴充功能的串流。
seo-title: 無延伸串流
title: 無延伸串流
uuid: c69ba62b-a940-4211-920d-2e559849fd6d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 無延伸串流{#extensionless-streams}

瀏覽器TVSDK目前支援播放清單和片段不含擴充功能的串流。

## 片段層級 {#section_0E035129501D4A77BBC14192D8A53A86}

瀏覽器TVSDK會剖析回應的前幾個位元組，以偵測無延伸片段的內容類型。 如果未偵測到有效的內容類型，瀏覽器TVSDK將會擲回錯誤。

## 資訊清單層級 {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

瀏覽器TVSDK使用 `mediaResource.resourceType` 方法中傳遞的參數 `replaceCurrentResource` 來偵測資訊清單URL的內容類型。 如需詳細資訊，請參閱 `AdobePSDK.MediaPlayer` 類別。

在UI Framework播放器中，您可以指定媒體資源中的資源類型，如下所示：

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

如果 `resourceType` 未提供，UI框架會根據資源URL擴展確定資源類型，然後將其傳遞到方 `replaceCurrentResource` 法。

>[!TIP]
>
>若為無擴充功能的資訊清單，請確 `resourceType` 定在UI架構中載入資源時一律傳遞。

