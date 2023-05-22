---
description: 302重定向優化將302個重定向響應的數量減到最少，這樣您的應用程式就可以更有效地平衡負載。
title: 禁用或啟用302重定向優化
exl-id: b1bdb6d6-b34d-4e0a-8c96-7fd4ce77b5c9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# HTTP 302重定向優化 {#http-302-redirect-optimization}

302重定向優化將302個重定向響應的數量減到最少，這樣您的應用程式就可以更有效地平衡負載。

如果重定向主清單請求，並且在您的播放器中啟用了302優化，則對該清單中資產的後續請求將使用最終域位置，這樣可避免額外的302響應。

預設情況下啟用此功能，您可以更改此設定。

## 禁用或啟用302重定向優化{#disable-or-enable-redirect-optimization}

使用 `useRedirectedUrl` 屬性以開啟(true)或關閉(false)重定向。
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
