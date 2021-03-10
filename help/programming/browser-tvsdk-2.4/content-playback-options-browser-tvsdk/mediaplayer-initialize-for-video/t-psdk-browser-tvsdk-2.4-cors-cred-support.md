---
description: 支援XMLHttpRequests中的withCredentials屬性，可讓跨原始資源共用(CORS)請求包含多種請求類型的目標網域Cookie。
keywords: CORS;cross origin；資源共用；cookies;withCredentials
title: 跨來源資源共用
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# 跨原始資源共用{#cross-origin-resource-sharing}

支援XMLHttpRequests中的withCredentials屬性，可讓跨原始資源共用(CORS)請求包含多種請求類型的目標網域Cookie。

當用戶端要求資訊清單、區段或金鑰時，伺服器可設定用戶端必須傳遞的Cookie，才能進行後續的要求。 若要允許讀取和寫入Cookie，用戶端必須針對跨來源要求將`withCredentials`屬性設為`true`。

要在播放給定媒體資源時啟用`withCredentials`對大多數類型請求的支援：

1. 建立`CORSConfig`對象。

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. 將`corsConfig`附加到`NetworkConfiguration`對象，並將`useCookieHeaderForAllRequests`設定為`true`。

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. 在`MediaPlayerItemConfig`對象中設定`networkConfig`。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. 將`MediaPlayerItemConfig`傳遞至`MediaPlayer.replaceCurrentResource`方法。

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>`useCookieHeaderForAllRequests`標幟不會影響授權要求。 要為許可證請求將`withCredentials`屬性設定為`true`，您必須在保護資料中設定`withCredentials`屬性，或在保護資料的`httpRequestHeaders`中指定授權密鑰。 例如：

```
# Example 1 
{ 
    "com.widevine.alpha": {  
        "withCredentials":true,  
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i]" } 
} 
 
# Example 2 
{ 
    "com.widevine.alpha": { 
        "httpRequestHeaders": {  
            "authorization": "true"  
            }, 
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i>]" }
        } 
}
```

此標幟不會影響授權要求，因為有些伺服器會在回應中將`Access-Control-Allow-Origin`欄位設為萬用字元(&#39;*&#39;)。 但是，當憑證標幟設定為`true`時，萬用字元無法用於`Access-Control-Allow-Origin`。 如果您針對所有類型的請求將`useCookieHeaderForAllRequests`設為`true`，則授權請求可能會出現下列錯誤：

請記住下列資訊：

* 當具有`withCredentials=true`的呼叫失敗時，瀏覽器TVSDK會重試沒有`withCredentials`的呼叫。
* 使用`networkConfiguration.useCookieHeaderForAllRequests=false`進行呼叫時，會發出XHR請求，而不使用`withCredentials`屬性。