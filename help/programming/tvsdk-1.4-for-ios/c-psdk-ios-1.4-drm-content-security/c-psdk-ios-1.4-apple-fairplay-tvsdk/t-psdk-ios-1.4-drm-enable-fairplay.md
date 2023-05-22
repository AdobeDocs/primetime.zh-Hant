---
description: 您可以在TVSDK應用程式中實施Apple的DRM解決方案FairPlay Streaming。
title: 在TVSDK應用程式中啟用Apple公平播放
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 在TVSDK應用程式中啟用Apple公平播放{#enable-apple-fairplay-in-tvsdk-applications}

您可以在TVSDK應用程式中實施Apple的DRM解決方案FairPlay Streaming。

1. 通過實施FairPlay客戶資源載入器建立 `PTAVAssetResourceLoaderDelegate`。

   有關詳細資訊，請參見 [AppleTVSDK應用中的FairPlay](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)。

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
