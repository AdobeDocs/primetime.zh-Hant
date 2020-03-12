---
description: 支援XMLHttpRequests中的withCredentials屬性，可讓跨原始資源共用(CORS)請求包含多種請求類型的目標網域Cookie。
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
seo-description: 支援XMLHttpRequests中的withCredentials屬性，可讓跨原始資源共用(CORS)請求包含多種請求類型的目標網域Cookie。
seo-title: 跨來源資源共用
title: 跨來源資源共用
uuid: e788b542-d4ac-48aa-91e2-1e88068cbba1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 跨來源資源共用 {#cross-origin-resource-sharing}

支援XMLHttpRequests中的withCredentials屬性，可讓跨原始資源共用(CORS)請求包含多種請求類型的目標網域Cookie。

當用戶端要求資訊清單、區段或金鑰時，伺服器可設定用戶端必須傳遞的Cookie，才能進行後續的要求。 若要允許讀取和寫入Cookie，用戶端必須將屬性 `withCredentials` 設定為跨 `true` 原始碼請求。

若要在播 `withCredentials` 放指定的媒體資源時啟用對大多數類型請求的支援：

1. 建立對 `CORSConfig` 像。

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. 將對 `corsConfig` 像附加 `NetworkConfiguration` 並設定 `useCookieHeaderForAllRequests` 為 `true`。

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. 在對 `networkConfig` 像中設 `MediaPlayerItemConfig` 置。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. 傳 `MediaPlayerItemConfig` 遞至方 `MediaPlayer.replaceCurrentResource` 法。

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>此標 `useCookieHeaderForAllRequests` 幟不會影響授權要求。 要將屬 `withCredentials` 性設定為許 `true` 可請求，必須在保護資料中設定屬性，或在保護資料中指定 `withCredentials``httpRequestHeaders` 授權密鑰。 例如：

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

此標幟不會影響授權要求，因為有些伺服器會在回應 `Access-Control-Allow-Origin` 時將欄位設為萬用字元(&#39;*&#39;)。 但是，當憑證標幟設定為 `true`時，萬用字元無法用於 `Access-Control-Allow-Origin`。 如果您針對所 `useCookieHeaderForAllRequests` 有類 `true` 型的請求設定，則授權請求可能會出現下列錯誤：

請記住下列資訊：

* 當呼叫失敗時， `withCredentials=true` 瀏覽器TVSDK會重試呼叫，而不 `withCredentials`會。
* 使用呼叫時，會 `networkConfiguration.useCookieHeaderForAllRequests=false`發出XHR請求，而不含 `withCredentials` 屬性。