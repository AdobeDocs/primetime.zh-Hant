---
description: 您可以在TVSDK應用程式中實作Apple FairPlay串流（Apple的DRM解決方案）。
seo-description: 您可以在TVSDK應用程式中實作Apple FairPlay串流（Apple的DRM解決方案）。
seo-title: 在TVSDK應用程式中啟用Apple FairPlay
title: 在TVSDK應用程式中啟用Apple FairPlay
uuid: fafffdb9-09f9-45fb-9957-3c6e95ed55f9
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 在TVSDK應用程式中啟用Apple FairPlay{#enable-apple-fairplay-in-tvsdk-applications}

您可以在TVSDK應用程式中實作Apple FairPlay串流（Apple的DRM解決方案）。

1. 透過實作，建立您的FairPlay客戶資源載入器 `PTAVAssetResourceLoaderDelegate`。

   如需詳細資訊，請參 [閱TVSDK應用程式中的Apple FairPlay](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)。

   >[!NOTE]
   >
   >請確定您遵循 *FairPlay串流程式指南* (FairPlayStreaming_PG.pdf *)中的指示，此指示包含在* FairPlay Server SDK中，以開發FPS感應應用程式 [](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip))。

   該方 `resourceLoader:shouldWaitForLoadingOfRequestedResource` 法等效於中的內容 `AVAssetResourceLoaderDelegate`。

   >[!IMPORTANT] {imporication=&quot;high&quot;}
   >
   >在ExpressPlay授權伺服器案例中，若要播放內容，請將ExpressPlay FairPlay伺服器授權要求URL中的URL配置從 `skd://` 變 `https://` 更為( `https://`或)。

1. 向註冊 *FairPlay* Customer Resource Loader `registerPTAVAssetResourceLoader`。

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您自行編寫FairPlay授權伺服器，或您使用協力廠商FairPlay授權伺服器，請洽詢您的授權伺服器廠商，以判斷您的授權伺服器URL、格式設定及任何其他需求。
