---
description: 若要在TVSDK應用程式中實作FairPlay串流，您需要編寫資源載入器，這會傳送授權贏取請求至您的FairPlay串流伺服器。
title: TVSDK應用程式中的Apple FairPlay
exl-id: 83fdc75b-f736-4091-ab80-e7f6e9723482
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# TVSDK應用程式中的Apple FairPlay  {#apple-fairplay-in-tvsdk-applications}

若要在TVSDK應用程式中實作FairPlay串流，您需要編寫資源載入器，這會傳送授權贏取請求至您的FairPlay串流伺服器。

資源載入器程式碼負責下列工作：

1. 決定要將授權贏取要求傳送至何處。
1. 格式化請求。
1. 提供必要資訊給伺服器，讓伺服器可以決定是否應允許該要求。

例如，如果您使用ExpressPlay提供的Adobe Primetime Cloud DRM，資源載入器會將要求傳送至：

```
https://fp-gen.service.expressplay.com
```

資源載入器會格式化要求，並附加授權播放的ExpressPlay權杖至URL。 取得ExpressPlay權杖時，需要考量幾個選項。 這些選項由您封裝內容的方式決定。

封裝內容時，封裝程式會插入 `skd:` M3U8資訊清單中的URL。 晚於 `skd:` 輸入項，您可以將任何資料放入資訊清單中。 您可以在應用程式程式碼中使用此資料，以完成上述工作。 例如，您可以使用 `skd:{content_id}` 讓您的應用程式能夠判斷正在播放的內容的ID，並請求該特定內容的Token。 例如，您也可以使用 `skd:{entitlement_server_url}?cid={content_id}`，因此您的應用程式不需要將授權伺服器URL硬式編碼。

您可能不需要任何資訊於 `skd:` URL，表示當播放開始時，您已經透過其他管道知道內容ID。 第二個範例是測試設定的理想解決方案，但您也可以在生產環境中使用。

>[!TIP]
>
>由您決定 `skd:`.

您的內容是透過以下方式取得： `skd:` 通訊協定，但您的授權請求使用 `https:`. 處理這些通訊協定最常見的選項包括：

* **端對端播放的初始測試** 封裝內容時，請選取 `skd:` URL。 測試您的應用程式時，請手動從ExpressPlay取得授權，並以硬式編碼撰寫授權(需在 `https:` URL)和內容URL。

   例如：

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **大多數其他案例** 封裝內容時，請選取 `skd:` 唯一代表內容ID的URL。 在您的載入器中，剖析 `skd:` url，將其傳送至您的伺服器以取得Token，並使用產生的Token做為URL。

   例如：

   ```
   - (BOOL)resourceLoader:(AVAssetResourceLoader *)resourceLoader  
         shouldWaitForLoadingOfRequestedResource:(AVAssetResourceLoadingRequest *)loadingRequest { 
       NSURL *url = [[loadingRequest request] URL]; 
       if (![[url scheme] isEqual:@"skd"]) 
           return NO; 
   
       NSString *strUrl = [url absoluteString]; 
       NSLog(@"url is: %@", strUrl); 
   
       strUrl = [strUrl stringByReplacingOccurrencesOfString:@"skd://" withString:@"https://"]; 
   
       NSData *assetId; 
   
       NSData *requestBytes; 
       NSError* error = nil; 
       BOOL handled = NO; 
   
       NSData  *responseData = nil; 
   
       assetId = getMyAssetIdentifierFromURL(url); 
   
       /* Usecase 1: "On Premise Fairplay Server" 
        * Set the strUrl to the OnPremise Fairplay Server Url. The OnPremise Fairplay  
        * Server Url is either hardcoded in the App or derived from strUrl. 
        */ 
   #if 0  
       // Insert your use case 1 codes here: 
       // strUrl = getOnPremiseServerUrl(strUrl, assetId); 
   #endif // 
   
       /* Usecase 2: The strUrl is the entitlement server. 
        * Send assetId to the entitlement server; if the user is allowed to playback  
        * the content, the entitlement server will send back an ExpressPlay Token Url. 
        */ 
   
   #if 0 
       // The hardcoded SEES server: 
       strUrl = @"https://10.0.248.85:8080/sees/SEESServlet"; 
   
       // You can use the following code to simulate a device binding entitlement  
       // request:  
       // First, invoke getExpressPlayTokenUrlFromEntilementServer with  
       // bEnforceDeviceID set to false. When you play the content, the device_id  
       // will be registered on the ExpressPlay Server.  Now change code to set  
       // bEnforceDeviceID to true, and rerun the program. The ExpressPlay token  
       // sent back by the SEES server will be device bound. 
   
       // The strUrl returned below is the ExpressPlay Token URL. 
       strUrl = getExpressPlayTokenUrlFromEntilementServer(strUrl, assetId, true, &error); 
   #endif 
   
       /* Usecase 3: The strUrl is already the ExpressPlay Token Url. 
        */ 
   
       // Read in the certificate 
       NSLog(@"Get Application Certificate"); 
       NSString* certPath = [[NSBundle mainBundle] pathForResource:@"my_certificate.cer"  
                                                            ofType:nil]; 
   
       NSData *appCert = [NSData dataWithContentsOfFile:certPath]; 
   
       // To create the request blob for the server: 
       requestBytes = [loadingRequest streamingContentKeyRequestDataForApp: appCert 
                                                         contentIdentifier:assetId  
                                                                   options:nil  
                                                                     error:&error]; 
       if (requestBytes == nil) { 
           NSLog(@"Error creating server request: %@", error); 
           return false; 
       } 
       // Per the specification, send requestBytes along with the assetId to the Key 
       // Server and obtain the response. 
       NSError *err; 
   
       responseData = getCKCFromExpressPlayService( strUrl, requestBytes, assetId, &err); 
   
       if (responseData != nil) { 
           NSLog(@"Get response data: "); 
           [loadingRequest finishLoadingWithResponse:nil  
                                                data:(NSData *)responseData 
                                            redirect:nil]; 
       } 
       else { 
           [loadingRequest finishLoadingWithError:err]; 
           NSLog(@"bad key response"); 
       } 
       handled = YES; 
   bail: 
       return handled; 
   
   }
   ```

## 在TVSDK應用程式中啟用Apple FairPlay{#enable-apple-fairplay-in-tvsdk-applications}

您可以在TVSDK應用程式中實作Apple FairPlay串流(Apple的DRM解決方案)。

1. 透過實作來建立FairPlay客戶資源載入器 `PTAVAssetResourceLoaderDelegate`.

   如需詳細資訊，請參閱 [TVSDK應用程式中的Apple FairPlay](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >請務必遵循 *FairPlay串流節目指南* ( *FairPlayStreaming_PG.pdf*)，這包含在 [用於開發FPS感知應用程式的FairPlay Server SDK](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip))。

   此 `resourceLoader:shouldWaitForLoadingOfRequestedResource` 方法等同於中的 `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >在ExpressPlay授權伺服器情境中，若要播放內容，請將ExpressPlay FairPlay伺服器授權請求URL中的URL配置變更為 `skd://` 至 `https://` (或 `https://`)。

1. 註冊 *Fairplay* 客戶資源載入器，搭配 `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您撰寫了自己的FairPlay授權伺服器，或您使用的是協力廠商FairPlay授權伺服器，請洽詢授權伺服器廠商，以決定您的授權伺服器URL、格式及任何其他需求。
