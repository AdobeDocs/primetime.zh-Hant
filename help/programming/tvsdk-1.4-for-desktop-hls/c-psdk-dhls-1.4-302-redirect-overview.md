---
description: 302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效地進行負載平衡。
title: HTTP 302重新導向最佳化
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# HTTP 302重新導向最佳化{#http-redirect-optimization}

302重新導向最佳化可將302重新導向回應的數量降至最低，讓您的應用程式更有效地進行負載平衡。

如果主要資訊清單要求重新導向，且您的播放器已啟用302最佳化，則從該資訊清單對資產發出的後續要求將使用最終網域位置，以避免額外的302回應。

此功能預設為停用，您可以變更此設定。

如果啟用此功能，則只有在 *全部* 下列條件之一為true，否則不會發生重新導向最佳化，且會繼續發生302個回應：

* 您的應用程式是針對AdobeFlash Player11.8編譯的，使用 `-swf-version` 21或更高。
* 您的使用者已安裝AdobeFlash Player11.8或更新版本。

>[!IMPORTANT]
>
>若要確保Cookie能連同廣告要求一起傳遞，請停用302重新導向。 啟用302重新導向時，廣告要求可能會重新導向至與Cookie來源網域不同的網域。

## 停用或啟用302重新導向最佳化 {#section_D6687FC44C61446F878008B629A5FA19}

使用 `useRedirectedUrl` 屬性以開啟(true)或關閉(false)302重新導向。

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
