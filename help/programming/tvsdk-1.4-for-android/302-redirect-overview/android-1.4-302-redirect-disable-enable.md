---
description: 302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效率地平衡負載。
title: 停用或啟用302重新導向最佳化
exl-id: b1bdb6d6-b34d-4e0a-8c96-7fd4ce77b5c9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# HTTP 302重新導向最佳化 {#http-302-redirect-optimization}

302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效率地平衡負載。

如果重新導向主要資訊清單請求，並在播放器中啟用302最佳化，則從該資訊清單對資產發出的後續請求將使用最終網域位置，這會避免額外302個回應。

此功能預設為啟用，您可以變更此設定。

## 停用或啟用302重新導向最佳化{#disable-or-enable-redirect-optimization}

使用 `useRedirectedUrl` 屬性以開啟302重新導向(true)或關閉(false)。
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
