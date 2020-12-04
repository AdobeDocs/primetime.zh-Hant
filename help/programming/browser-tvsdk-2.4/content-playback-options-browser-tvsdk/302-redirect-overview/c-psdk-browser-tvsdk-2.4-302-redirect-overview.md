---
description: 302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。
seo-description: 302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。
seo-title: HTTP 302重新導向最佳化
title: HTTP 302重新導向最佳化
uuid: d3009c6c-320a-4c0f-b6ba-bf6473049823
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# HTTP 302重新導向最佳化{#http-redirect-optimization}

302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。

如果重新導向主資訊清單請求，而您的播放器中已啟用302最佳化，則後續從該資訊清單請求資產時，會使用最終網域位置，以避免額外302個回應。 此功能預設為啟用，您可以變更此設定。

>[!IMPORTANT]
>
>只有在支援`XMLHttpRequest`物件中`responseURL`屬性的認證瀏覽器才支援此功能。

若是Flash備援，請記住下列資訊：

* 您的使用者必須已安裝Adobe Flash Player 23版或更新版本。
* 如果停用串流完整性，則僅認證的瀏覽器才支援302重新導向。

## 停用302重新導向最佳化{#disabling-redirect-optimization}

您可以使用useRedirectedUrl屬性來啟用302重新導向(true)或停用(false)。

例如：

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
