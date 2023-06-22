---
description: 302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效率地平衡負載。
title: HTTP 302重新導向最佳化
exl-id: 80d5d38d-c998-4fc0-b527-b38e578d76e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# HTTP 302重新導向最佳化 {#http-redirect-optimization}

302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效率地平衡負載。

如果重新導向主要資訊清單請求，並在播放器中啟用302最佳化，則從該資訊清單對資產發出的後續請求將使用最終網域位置，這會避免額外302個回應。 此功能預設為啟用，您可以變更此設定。

>[!IMPORTANT]
>
>只有支援此功能的已認證瀏覽器才支援此功能 `responseURL` 中的屬性 `XMLHttpRequest` 物件。

如需Flash備援，請記住下列資訊：

* 您的使用者必須安裝AdobeFlash Player版本23或更新版本。
* 如果停用資料流完整性，則只有在認證的瀏覽器上才支援302重新導向。

## 停用302重新導向最佳化 {#disabling-redirect-optimization}

您可以使用useRedirectedUrl屬性來啟用302重新導向(true)或停用(false)。

例如：

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
