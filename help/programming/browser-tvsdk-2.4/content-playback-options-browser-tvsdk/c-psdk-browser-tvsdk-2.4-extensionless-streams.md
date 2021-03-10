---
description: 瀏覽器TVSDK目前支援播放清單和片段不含擴充功能的串流。
title: 無延伸串流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# 無擴展流{#extensionless-streams}

瀏覽器TVSDK目前支援播放清單和片段不含擴充功能的串流。

## 片段級別{#section_0E035129501D4A77BBC14192D8A53A86}

瀏覽器TVSDK會剖析回應的前幾個位元組，以偵測無延伸片段的內容類型。 如果未偵測到有效的內容類型，瀏覽器TVSDK將會擲回錯誤。

## 資訊清單層級{#section_AAD9EBAC883D4CC3A0133A45B555EECF}

瀏覽器TVSDK使用`replaceCurrentResource`方法中傳遞的`mediaResource.resourceType`參數來偵測資訊清單URL的內容類型。 如需詳細資訊，請參閱`AdobePSDK.MediaPlayer`類別。

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

如果未提供`resourceType`,UI框架將根據資源URL擴展確定資源類型，然後將該資源類型傳遞至`replaceCurrentResource`方法。

>[!TIP]
>
>對於無延伸功能資訊清單，請確定在UI架構中載入資源時一律傳遞`resourceType`。

