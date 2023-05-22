---
description: 302重定向優化將302個重定向響應的數量減到最少，這樣您的應用程式就可以更有效地平衡負載。
title: HTTP 302重定向優化
exl-id: 9b9d98ae-a509-47dc-a5ac-6be9b0f214c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# HTTP 302重定向優化{#http-redirect-optimization}

302重定向優化將302個重定向響應的數量減到最少，這樣您的應用程式就可以更有效地平衡負載。

如果重定向主清單請求，並且在您的播放器中啟用了302優化，則對該清單中資產的後續請求將使用最終域位置，這樣可避免額外的302響應。

預設情況下禁用此功能，您可以更改此設定。

如果啟用此功能，則只有在 *全部* 符合下列條件的；否則，不會進行重定向優化，並且會繼續出現302個響應：

* 您的應用程式已編譯為AdobeFlash Player11.8，使用 `-swf-version` 21或更高。
* 您的最終用戶已安裝AdobeFlash Player11.8或更高版本。

>[!IMPORTANT]
>
>要確保Cookie與廣告請求一起傳遞，請禁用302重定向。 啟用302重定向後，廣告請求可能會重定向到與Cookie的發源域不同的域。

## 禁用或啟用302重定向優化 {#section_D6687FC44C61446F878008B629A5FA19}

使用 `useRedirectedUrl` 屬性以開啟(true)或關閉(false)重定向。

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
