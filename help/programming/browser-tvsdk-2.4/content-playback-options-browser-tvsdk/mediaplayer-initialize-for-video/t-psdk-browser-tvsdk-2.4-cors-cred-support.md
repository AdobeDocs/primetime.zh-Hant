---
description: 支援XMLHttpRequests中的withCredentials屬性允許跨源資源共用(CORS)請求包含目標域的Cookie，以用於各種請求類型。
keywords: CORS；交叉源；資源共用；cookie;withCredentials
title: 跨源資源共用
exl-id: 02826c87-b0c6-495b-a17d-67c5693a9772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 跨源資源共用 {#cross-origin-resource-sharing}

支援XMLHttpRequests中的withCredentials屬性允許跨源資源共用(CORS)請求包含目標域的Cookie，以用於各種請求類型。

當客戶端請求清單、段或密鑰時，伺服器可以設定客戶端必須為後續請求傳遞的cookie。 要允許讀取和寫入Cookie，客戶端必須設定 `withCredentials` 屬性 `true` 源間請求。

啟用 `withCredentials` 在播放給定媒體資源時支援大多數類型的請求：

1. 建立 `CORSConfig` 的雙曲餘切值。

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. 附加 `corsConfig` 到 `NetworkConfiguration` 對象和集 `useCookieHeaderForAllRequests` 至 `true`。

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. 設定 `networkConfig` 的 `MediaPlayerItemConfig` 的雙曲餘切值。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. 通過 `MediaPlayerItemConfig` 到 `MediaPlayer.replaceCurrentResource` 的雙曲餘切值。

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>的 `useCookieHeaderForAllRequests` 標誌不影響許可證請求。 設定 `withCredentials` 屬性 `true` 對於許可證請求，必須設定 `withCredentials` 屬性或在 `httpRequestHeaders` 保護資料。 例如：

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

該標誌不影響許可證請求，因為某些伺服器設定了 `Access-Control-Allow-Origin` 欄位到通配符(&#39;&#42;&quot;)的回答。 但是，當憑據標誌設定為 `true`，無法在中使用通配符 `Access-Control-Allow-Origin`。 如果設定 `useCookieHeaderForAllRequests` 至 `true` 對於所有類型的請求，您可能會看到許可證請求出現以下錯誤：

記住以下資訊：

* 當呼叫 `withCredentials=true` 失敗，瀏覽器TVSDK將重試調用， `withCredentials`。
* 呼叫時 `networkConfiguration.useCookieHeaderForAllRequests=false`, XHR請求在 `withCredentials` 屬性。
