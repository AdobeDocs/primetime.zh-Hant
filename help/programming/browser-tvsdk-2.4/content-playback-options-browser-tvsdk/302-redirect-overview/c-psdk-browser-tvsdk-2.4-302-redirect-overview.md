---
description: 302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效地進行負載平衡。
title: HTTP 302重新導向最佳化
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# HTTP 302重新導向最佳化 {#http-redirect-optimization}

302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效地進行負載平衡。

如果主要資訊清單要求重新導向，且您的播放器已啟用302最佳化，則從該資訊清單對資產發出的後續要求將使用最終網域位置，以避免額外的302回應。 此功能預設為啟用，您可以變更此設定。

>[!IMPORTANT]
>
>只有支援此功能的已認證瀏覽器才支援 `responseURL` 中的屬性 `XMLHttpRequest` 物件。

如需Flash遞補，請記住以下資訊：

* 您的使用者必須安裝AdobeFlash Player版本23或更新版本。
* 如果停用資料流完整性，則只有在已驗證的瀏覽器上才支援302重新導向。

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
