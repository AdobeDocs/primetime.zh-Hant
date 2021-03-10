---
description: 您可以使用Adobe的Offline Packager，為Primetime Cloud DRM（由ExpressPlay提供支援）支援的任何DRM解決方案準備內容。
title: Primetime Packager / Cloud DRM / TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

您可以使用Adobe的Offline Packager，為Primetime Cloud DRM（由ExpressPlay提供支援）支援的任何DRM解決方案準備內容。

這組說明假設您已經設定ExpressPlay管理帳戶：[Primetime DRM Cloud快速入門](../../../multi-drm-workflows/quick-start/quick-overview.md)。
1. 選擇用於封裝內容的基礎架構。 Primetime Packager支援命令列和以組態為基礎的內容封裝，以便與FairPlay、Widevine和PlayReady DRM搭配使用。 TVSDK目前支援下列格式和加密（管道中包含更多）:

   * DASH(CENC)/ PlayReady,Widevine —— 適用於HTML5
   * HLS / FairPlay, Access —— 適用於iOS

1. 選擇密鑰管理系統(KMS):

   * 使用ExpressPlay的KMS（[ExpressPlay密鑰儲存](https://www.expressplay.com/developer/key-storage/)）;此系統透過ExpressPlay的REST風格API管理您的內容金鑰。

      或者……

   * 設定您自己的KMS 建立內容索引鍵資料庫，可由Content-ID選取。

      無論哪種情況，KMS都管理內容密鑰的供應，每個密鑰都具有關聯的內容ID。

1. 封裝您的內容。 有了Primetime Packager，您就可以針對特定DRM解決方案或多個DRM解決方案封裝內容。

   以下示例命令顯示了為不同DRM解決方案打包內容的一些示例：

   * [Widevine with Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19) (generats MPD file):

      ```
      java -jar OfflinePackager.jar \ 
        -in_path [ 
        <your_content.mp4>] \ 
        -out_type dash \ 
        -out_path [ 
        <your_out_file_path>] \ 
        -drm \ 
        -drm_sys WIDEVINE \ 
        -key_file_path "creds/widevine_key.bin" \ 
        -widevine_key_id [ 
        <some_keyID>] \ 
        -widevine_content_id [ 
        <some_content-ID] \ 
        -widevine_header provider:intertrust#content_id:2a
      ```

   * [FairPlay with Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) （產生M3U8檔案）:

      ```
      java -jar OfflinePackager.jar  
        -in_path [ 
        <your_content.mp4>]  
        -out_type hls  
        -out_path [ 
        <your_out_file_path>]  
        -drm  
        -drm_sys FAIRPLAY  
        -key_file_path "creds/fairplay_key.bin"  
        -key_url "user_provided_value"
      ```

      >[!NOTE]
      >
      >複製`key_url`值的方式與M3U8檔案相同。

1. 建立「店面伺服器」。

       店面伺服器需要處理以下操作：
   
   1. 客戶選擇內容。 此實作需要包含端點，讓用戶端為特定內容ID請求內容Token。
   1. 客戶權益
   1. 來自用戶端的授權Token(ExpressPlay)要求（[ExpressPlay授權Token要求／回應參考](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md)）

1. 建立您的客戶。

       客戶端應包括對店面伺服器的呼叫。Adobe建議用戶在選擇某些內容後，以及用戶通過身份驗證後，客戶端調用店面。 然後，將從ExpressPlay傳回的Token傳遞至您的播放器，以用於授權要求。 實作播放器DRM元件的簡介如下：
   
   * [HTML5的瀏覽器TVSDK](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 有了授權Token，用戶端現在可以從Token衍生要求URL，並對ExpressPlay提出授權要求，然後為使用者播放選取的內容。
