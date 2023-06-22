---
description: 302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效率地平衡負載。
title: HTTP 302重新導向最佳化
exl-id: 9b9d98ae-a509-47dc-a5ac-6be9b0f214c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# HTTP 302重新導向最佳化{#http-redirect-optimization}

302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效率地平衡負載。

如果重新導向主要資訊清單請求，並在播放器中啟用302最佳化，則從該資訊清單對資產發出的後續請求將使用最終網域位置，這會避免額外302個回應。

此功能預設為停用，您可以變更此設定。

如果您啟用此功能，只有在 *全部* 下列條件中之一項為true，否則不會發生重新導向最佳化，且會持續發生302個回應：

* 您的應用程式已針對AdobeFlash Player11.8編譯，使用 `-swf-version` 21或更高。
* 您的使用者已安裝AdobeFlash Player11.8或更新版本。

>[!IMPORTANT]
>
>若要確保Cookie可透過廣告請求傳遞，請停用302重新導向。 啟用302重新導向時，廣告請求可能會被重新導向到與Cookie來源網域不同的網域。

## 停用或啟用302重新導向最佳化 {#section_D6687FC44C61446F878008B629A5FA19}

使用 `useRedirectedUrl` 屬性以開啟302重新導向(true)或關閉(false)。

<!--<a id="example_B886777252B745AAB48B1FCC42C97A25"></a>-->

例如：

```
// Set useRedirectedUrl property to true 
var networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = true; 
  
//Set NetworkConfiguration as Metadata: 
var result:Metadata = new Metadata(); 
result.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                   networkConfiguration); 
  
var mediaResource = new MediaResource( url, MediaResourceType.HLS, result); 
  
// load the resource 
mediaPlayer.replaceCurrentResource( mediaResource, mediaPlayerItemConfig );
```
