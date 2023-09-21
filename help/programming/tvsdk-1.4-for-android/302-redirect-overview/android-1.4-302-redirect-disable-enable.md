---
description: 302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效地進行負載平衡。
title: 停用或啟用302重新導向最佳化
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# HTTP 302重新導向最佳化 {#http-302-redirect-optimization}

302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效地進行負載平衡。

如果主要資訊清單要求重新導向，且您的播放器已啟用302最佳化，則從該資訊清單對資產發出的後續要求將使用最終網域位置，以避免額外的302回應。

此功能預設為啟用，您可以變更此設定。

## 停用或啟用302重新導向最佳化{#disable-or-enable-redirect-optimization}

使用 `useRedirectedUrl` 屬性以開啟(true)或關閉(false)302重新導向。
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
