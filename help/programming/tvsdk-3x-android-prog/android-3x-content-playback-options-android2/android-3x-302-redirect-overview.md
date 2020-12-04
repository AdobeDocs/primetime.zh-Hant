---
description: 302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。
seo-description: 302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。
seo-title: HTTP 302重新導向最佳化
title: HTTP 302重新導向最佳化
uuid: 91ed8919-a3c1-4e57-9eaf-e3ba430de35f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 1%

---


# HTTP 302重新導向最佳化{#http-redirect-optimization}

302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。

如果重新導向主資訊清單請求，而您的播放器中已啟用302最佳化，則後續從該資訊清單請求資產時，會使用最終網域位置，以避免額外302個回應。 此功能預設為啟用，您可以變更此設定。

## 停用或啟用302重新導向最佳化{#section_8977448B268E41D69A8F75B60EB9DA3B}

使用`useRedirectedUrl`屬性開啟(`true`)或關閉(`false`)302重新導向。

<!--<a id="example_888749F70C8A43279D06A29BD68E7E4D"></a>-->

例如：

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration on MediaPlayerItemConfig 
MediaPlayerItemConfig config = new MediaPlayerItemConfig (); 
config.setNetworkConfiguration(networkConfiguration); 
 
//Use this config when loading the MediaPlayerItem or calling replaceCurrentResource
```
