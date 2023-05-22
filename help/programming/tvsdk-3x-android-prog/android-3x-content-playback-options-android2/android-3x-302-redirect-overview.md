---
description: 302重定向優化將302個重定向響應的數量減到最少，這樣您的應用程式就可以更有效地平衡負載。
title: HTTP 302重定向優化
exl-id: a238e90f-3aa1-486b-b57f-d543e4c94b2e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# HTTP 302重定向優化 {#http-redirect-optimization}

302重定向優化將302個重定向響應的數量減到最少，這樣您的應用程式就可以更有效地平衡負載。

如果重定向主清單請求，並且在您的播放器中啟用了302優化，則對該清單中資產的後續請求將使用最終域位置，這樣可避免額外的302響應。 預設情況下啟用此功能，您可以更改此設定。

## 禁用或啟用302重定向優化 {#section_8977448B268E41D69A8F75B60EB9DA3B}

使用 `useRedirectedUrl` 開啟302重定向的屬性( `true`)或關( `false`)。

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
