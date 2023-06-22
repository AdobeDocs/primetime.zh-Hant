---
description: XMLHttpRequests中對withCredentials屬性的支援可允許跨原始資源共用(CORS)請求包含各種請求型別的目標網域的Cookie。
keywords: CORS；跨來源；資源共用；Cookie；withCredentials
title: 跨原始資源共用
exl-id: 02826c87-b0c6-495b-a17d-67c5693a9772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 跨原始資源共用 {#cross-origin-resource-sharing}

XMLHttpRequests中對withCredentials屬性的支援可允許跨原始資源共用(CORS)請求包含各種請求型別的目標網域的Cookie。

當使用者端要求資訊清單、區段或金鑰時，伺服器可能會設定使用者端必須傳遞的Cookie，以供後續要求使用。 若要允許讀取和寫入Cookie，使用者端必須將 `withCredentials` 屬性至 `true` 跨原始碼請求時。

若要啟用 `withCredentials` 播放指定媒體資源時，支援大多數型別的要求：

1. 建立 `CORSConfig` 物件。

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. 附加 `corsConfig` 至 `NetworkConfiguration` 物件與集合 `useCookieHeaderForAllRequests` 至 `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. 設定 `networkConfig` 在 `MediaPlayerItemConfig` 物件。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. 通過 `MediaPlayerItemConfig` 至 `MediaPlayer.replaceCurrentResource` 方法。

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>此 `useCookieHeaderForAllRequests` 標幟不會影響授權要求。 若要設定 `withCredentials` 屬性至 `true` 對於授權請求，您必須將 `withCredentials` 保護資料中的屬性，或在 `httpRequestHeaders` 保護資料的URL。 例如：

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

此標幟不會影響授權請求，因為有些伺服器會設定 `Access-Control-Allow-Origin` 萬用字元的欄位(&#39;&#42;&#39;)進行回應。 但是，當認證標幟設定為 `true`，萬用字元不能用於 `Access-Control-Allow-Origin`. 如果您設定 `useCookieHeaderForAllRequests` 至 `true` 對於所有型別的請求，您可能會看到授權請求的以下錯誤：

請記住以下資訊：

* 當呼叫使用 `withCredentials=true` 失敗，瀏覽器TVSDK會重試呼叫，但不執行 `withCredentials`.
* 使用進行呼叫時 `networkConfiguration.useCookieHeaderForAllRequests=false`，XHR請求不會在 `withCredentials` 屬性。
