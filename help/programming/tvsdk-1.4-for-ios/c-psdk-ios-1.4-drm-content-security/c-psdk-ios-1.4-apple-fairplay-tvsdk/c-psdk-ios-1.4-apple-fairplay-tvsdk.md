---
description: 若要在TVSDK應用程式中實作FairPlay串流，您需要編寫資源載入器，將授權取得要求傳送至FairPlay串流伺服器。
seo-description: 若要在TVSDK應用程式中實作FairPlay串流，您需要編寫資源載入器，將授權取得要求傳送至FairPlay串流伺服器。
seo-title: TVSDK應用程式中的Apple FairPlay
title: TVSDK應用程式中的Apple FairPlay
uuid: 4384d379-37cd-46c5-8c25-0cda16bdebb8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# TVSDK應用程式中的Apple FairPlay {#apple-fairplay-in-tvsdk-applications}

若要在TVSDK應用程式中實作FairPlay串流，您需要編寫資源載入器，將授權取得要求傳送至FairPlay串流伺服器。

資源載入程式碼負責以下任務：

1. 決定要在何處傳送授權取得要求。
1. 格式化請求。
1. 提供必要的資訊給伺服器，讓伺服器可決定是否允許要求。

例如，如果您使用ExpressPlay提供支援的Adobe Primetime Cloud DRM，您的資源載入器會將要求傳送至：

```
https://fp-gen.service.expressplay.com
```

「資源載入器」會格式化請求，並附加ExpressPlay Token，以授權播放至URL。 在取得ExpressPlay Token時，有幾個選項需要考慮。 這些選項取決於您封裝內容的方式。

當您封裝內容時，封裝程式會在您的M3U8資訊清單中插入`skd:` URL。 在`skd:`項目之後，您可將任何資料放入資訊清單中。 您可以在應用程式碼中使用此資料來完成上述工作。 例如，您可以使用`skd:{content_id}`，讓您的應用程式可以判斷所播放內容的ID，並請求該特定內容的Token。 例如，您也可以使用`skd:{entitlement_server_url}?cid={content_id}`，讓您的應用程式不需要硬式編碼權益伺服器URL。

當播放開始時，如果您已透過其他頻道瞭解內容ID，則可能不需要`skd:` URL中的任何資訊。 第二個範例是測試您設定的理想解決方案，但您也可以在生產環境中使用它。

>[!TIP]
>
>確定`skd:`的格式。

您的內容是使用`skd:`通訊協定取得，但您的授權要求使用`https:`。 處理這些通訊協定的最常用選項是：

* **端對端播放的初始測試封** 裝內容時，請選取 `skd:` URL。在測試您的應用程式時，請手動從ExpressPlay取得授權，並在載入器中硬式編碼授權(`https:` URL)和內容URL。

   例如：

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **大多數其** 他案例在封裝內容時，請選取唯 `skd:` 一代表內容ID的URL。在您的載入器中，剖析`skd:` URL，將它傳送至您的伺服器以取得Token，然後使用產生的Token做為URL。

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

您可以在TVSDK應用程式中實作Apple FairPlay串流（Apple的DRM解決方案）。

1. 實施`PTAVAssetResourceLoaderDelegate`以建立FairPlay客戶資源載入器。

   如需詳細資訊，請參閱「TVSDK應用程式中的[Apple FairPlay」。](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)

   >[!NOTE]
   >
   >請確定您遵循&#x200B;*FairPlay串流程式指南*(*FairPlayStreaming_PG.pdf*)中的指示，此指示包含在[FairPlay Server SDK中，以開發FPS-Aware App](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip))。

   `resourceLoader:shouldWaitForLoadingOfRequestedResource`方法等效於`AVAssetResourceLoaderDelegate`中的內容。

   >[!IMPORTANT]
   >
   >在ExpressPlay授權伺服器案例中，若要播放內容，請將ExpressPlay FairPlay伺服器授權要求URL中的URL配置從`skd://`變更為`https://`（或`https://`）。

1. 使用`registerPTAVAssetResourceLoader`註冊&#x200B;*FairPlay*&#x200B;客戶資源載入器。

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您自行編寫FairPlay授權伺服器，或您使用協力廠商FairPlay授權伺服器，請洽詢您的授權伺服器廠商，以判斷您的授權伺服器URL、格式設定及任何其他需求。