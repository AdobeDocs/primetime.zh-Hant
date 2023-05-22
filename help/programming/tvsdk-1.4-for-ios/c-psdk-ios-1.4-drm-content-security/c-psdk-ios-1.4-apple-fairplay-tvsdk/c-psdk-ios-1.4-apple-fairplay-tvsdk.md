---
description: 要在TVSDK應用中實施FairPlay流，您需要編寫資源載入器，該載入器向FairPlay流伺服器發送許可證獲取請求。
title: AppleTVSDK應用中的FairPlay
exl-id: 83fdc75b-f736-4091-ab80-e7f6e9723482
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# AppleTVSDK應用中的FairPlay  {#apple-fairplay-in-tvsdk-applications}

要在TVSDK應用中實施FairPlay流，您需要編寫資源載入器，該載入器向FairPlay流伺服器發送許可證獲取請求。

資源載入程式碼負責以下任務：

1. 確定在何處發送許可證獲取請求。
1. 格式化請求。
1. 向伺服器提供必要的資訊，以便伺服器能夠決定是否允許請求。

例如，如果您使用由ExpressPlay提供支援的Adobe的Mogine Cloud DRM，則資源載入器將請求發送給：

```
https://fp-gen.service.expressplay.com
```

資源載入器格式化請求並將授權回放的ExpressPlay令牌附加到URL。 獲取ExpressPlay令牌時，需要考慮幾個選項。 這些選項取決於您如何打包內容。

打包內容時，打包程式將插入 `skd:` M3U8清單中的URL。 在 `skd:` 條目，可將任何資料放入清單。 您可以在應用程式碼中使用此資料來完成上面列出的任務。 例如，您可以 `skd:{content_id}` 以便您的應用能夠確定正在播放的內容的ID，並請求該特定內容的令牌。 例如，您還可以 `skd:{entitlement_server_url}?cid={content_id}`，這樣您的應用就不需要硬編碼權利伺服器URL。

您可能不需要 `skd:` URL如果在播放開始時，您已通過其他頻道瞭解內容ID。 第二個示例是test設定的理想解決方案，但您也可以在生產環境中使用它。

>[!TIP]
>
>確定 `skd:`。

您的內容是通過 `skd:` 協定，但您的許可證請求使用 `https:`。 處理這些協定的最常用選項是：

* **端對端回放的初始測試** 打包內容時，選擇 `skd:` URL。 測試應用時，請手動從ExpressPlay獲取許可證並硬編碼許可證( `https:` URL)和載入程式中的內容URL。

   例如：

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **大多數其他案例** 打包內容時，選擇 `skd:` 唯一表示內容ID的URL。 在載入器中，分析 `skd:` URL，將其發送到伺服器以獲取令牌，並使用結果令牌作為URL。

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

## 在TVSDK應用程式中啟用Apple公平播放{#enable-apple-fairplay-in-tvsdk-applications}

您可以在TVSDK應用程式中實施Apple的DRM解決方案FairPlay Streaming。

1. 通過實施FairPlay客戶資源載入器建立 `PTAVAssetResourceLoaderDelegate`。

   有關詳細資訊，請參見 [AppleTVSDK應用中的FairPlay](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)。

   >[!NOTE]
   >
   >確保按照 *《 FairPlay流媒體節目指南》* ( *FairPlayStreaming_PG.pdf*)，包含於 [用於開發FPS感知應用的FairPlay Server SDK](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip))。

   的 `resourceLoader:shouldWaitForLoadingOfRequestedResource` 方法等效於中的內容 `AVAssetResourceLoaderDelegate`。

   >[!IMPORTANT]
   >
   >在ExpressPlay許可證伺服器方案中，要回放內容，請更改ExpressPlay FairPlay伺服器許可證請求URL中的URL方案 `skd://` 至 `https://` 或 `https://`)。

1. 註冊 *公平遊戲* 客戶資源載入器 `registerPTAVAssetResourceLoader`。

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您自己編寫了FairPlay許可證伺服器，或者您正在使用第三方FairPlay許可證伺服器，請咨詢許可證伺服器供應商以確定許可證伺服器URL、格式設定和任何其他要求。
