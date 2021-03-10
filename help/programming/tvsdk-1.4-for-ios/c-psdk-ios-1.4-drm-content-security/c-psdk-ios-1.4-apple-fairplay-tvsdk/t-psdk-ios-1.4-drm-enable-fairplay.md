---
description: 您可以在TVSDK應用程式中實作Apple FairPlay串流（Apple的DRM解決方案）。
title: 在TVSDK應用程式中啟用Apple FairPlay
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 在TVSDK應用程式中啟用Apple FairPlay{#enable-apple-fairplay-in-tvsdk-applications}

您可以在TVSDK應用程式中實作Apple FairPlay串流（Apple的DRM解決方案）。

1. 實施`PTAVAssetResourceLoaderDelegate`以建立FairPlay客戶資源載入器。

   如需詳細資訊，請參閱「TVSDK應用程式中的[Apple FairPlay」。](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)

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
