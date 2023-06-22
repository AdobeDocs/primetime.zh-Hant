---
description: 您可以在TVSDK應用程式中實作Apple FairPlay串流(Apple的DRM解決方案)。
title: 在TVSDK應用程式中啟用Apple FairPlay
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 在TVSDK應用程式中啟用Apple FairPlay{#enable-apple-fairplay-in-tvsdk-applications}

您可以在TVSDK應用程式中實作Apple FairPlay串流(Apple的DRM解決方案)。

1. 透過實作來建立FairPlay客戶資源載入器 `PTAVAssetResourceLoaderDelegate`.

   如需詳細資訊，請參閱 [TVSDK應用程式中的Apple FairPlay](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

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
