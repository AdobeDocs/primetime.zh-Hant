---
description: 302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。
seo-description: 302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。
seo-title: HTTP 302重新導向最佳化
title: HTTP 302重新導向最佳化
uuid: 58593d5f-a639-4d87-9589-dba6b2dbba38
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# HTTP 302重新導向最佳化{#http-redirect-optimization}

302重新導向最佳化可將302個重新導向回應的數目減到最少，讓您的應用程式更有效率地平衡負載。

如果重新導向主資訊清單請求，而您的播放器中已啟用302最佳化，則後續從該資訊清單請求資產時，會使用最終網域位置，以避免額外302個回應。

此功能預設為停用，您可以變更此設定。

如果您啟用此功能，則只有下列條件中的&#x200B;*all*&#x200B;為true時，此功能才能正常運作；否則，不會發生重新導向最佳化，而302個回應會持續發生：

* 您的應用程式是使用`-swf-version` 21或更新版本，編譯為Adobe Flash Player 11.8。
* 您的使用者已安裝Adobe Flash Player 11.8或更新版本。

>[!IMPORTANT]
>
>若要確保Cookie與廣告請求一起傳遞，請停用302重新導向。 啟用302重新導向後，廣告要求可能會重新導向至與Cookie產生來源網域不同的網域。

## 停用或啟用302重新導向最佳化{#section_D6687FC44C61446F878008B629A5FA19}

使用`useRedirectedUrl`屬性開啟(true)或關閉(false)302重新導向。

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

