---
description: 302重定向優化將302個重定向響應的數量減到最少，這樣您的應用程式就可以更有效地平衡負載。
title: HTTP 302重定向優化
exl-id: 80d5d38d-c998-4fc0-b527-b38e578d76e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# HTTP 302重定向優化 {#http-redirect-optimization}

302重定向優化將302個重定向響應的數量減到最少，這樣您的應用程式就可以更有效地平衡負載。

如果重定向主清單請求，並且在您的播放器中啟用了302優化，則對該清單中資產的後續請求將使用最終域位置，這樣可避免額外的302響應。 預設情況下啟用此功能，您可以更改此設定。

>[!IMPORTANT]
>
>僅在支援以下功能的認證瀏覽器中支援此功能 `responseURL` 屬性 `XMLHttpRequest` 的雙曲餘切值。

對於Flash回退，請記住以下資訊：

* 您的最終用戶必須安裝AdobeFlash Player版本23或更高版本。
* 如果禁用流完整性，則僅認證的瀏覽器支援302重定向。

## 禁用302重定向優化 {#disabling-redirect-optimization}

可以使用useRedirectedUrl屬性啟用302重定向(true)或禁用(false)。

例如：

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
