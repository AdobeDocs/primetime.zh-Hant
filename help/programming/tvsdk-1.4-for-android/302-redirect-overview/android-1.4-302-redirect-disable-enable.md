---
description: 302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。
seo-description: 302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。
seo-title: 停用或啟用302重新導向最佳化
title: 停用或啟用302重新導向最佳化
uuid: 7561839f-aec6-4a59-a07a-7e4fa043fdc2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# HTTP 302重新導向最佳化 {#http-302-redirect-optimization}

302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。

如果重新導向主資訊清單請求，而您的播放器中已啟用302最佳化，則後續從該資訊清單請求資產時，會使用最終網域位置，以避免額外302個回應。

此功能預設為啟用，您可以變更此設定。

## 停用或啟用302重新導向最佳化{#disable-or-enable-redirect-optimization}

使用屬 `useRedirectedUrl` 性開啟(true)或關閉(false)302重新導向。
例如：

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration as Metadata: 
MetadataNode resourceMetadata = new MetadataNode();  
resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                         networkConfiguration); 
 
//Call MediaResource.createFromURL to set the metadata: 
MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
  
//Load the resource 
mediaPlayer.replaceCurrentItem(resource);
```

