---
description: 302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效率地平衡負載。
title: HTTP 302重新導向最佳化
exl-id: fdbdc2b4-6c1a-4ab1-80e2-b5e079ffa906
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# HTTP 302重新導向最佳化 {#http-redirect-optimization}

302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效率地平衡負載。

如果重新導向主要資訊清單請求，並在播放器中啟用302最佳化，則從該資訊清單對資產發出的後續請求將使用最終網域位置，這會避免額外302個回應。 此功能預設為啟用，您可以變更此設定。

## 停用或啟用302重新導向最佳化 {#section_8977448B268E41D69A8F75B60EB9DA3B}

使用 `useRedirectedUrl` 要開啟302重新導向的屬性( `true`)或關閉( `false`)。

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
