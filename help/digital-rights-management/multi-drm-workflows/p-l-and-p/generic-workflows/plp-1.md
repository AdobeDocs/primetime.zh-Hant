---
description: 您可以使用Adobe的Offline Packager，為Primetime Cloud DRM支援的任何DRM解決方案（由ExpressPlay提供技術支援）準備內容。
title: Primetime Packager / Cloud DRM / TVSDK
exl-id: 2055c18b-62de-41bf-9644-f366609e0198
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

您可以使用Adobe的Offline Packager，為Primetime Cloud DRM支援的任何DRM解決方案（由ExpressPlay提供技術支援）準備內容。

這組指示假設您已設定ExpressPlay管理員帳戶： [Primetime DRM雲端快速入門](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. 選擇用於封裝內容的基礎結構。 Primetime Packager支援命令列式與組態式內容封裝，以搭配FairPlay、Widevine和PlayReady DRM使用。 TVSDK目前支援下列格式和加密（管道中提供詳細資訊）：

   * DASH (CENC) / PlayReady、Widevine -HTML5
   * HLS / FairPlay、Access — 適用於iOS

1. 選擇金鑰管理系統(KMS)：

   * 使用ExpressPlay的KMS ( [ExpressPlay金鑰儲存](https://www.expressplay.com/developer/key-storage/))；此系統透過ExpressPlay的RESTful API管理您的內容金鑰。

      或……

   * 設定您自己的KMS。 建立內容金鑰的資料庫，可由Content-ID選取。

      無論是哪種情況，KMS都會管理內容金鑰的供給，每個金鑰都有一個相關聯的內容ID。

1. 封裝您的內容。 透過Primetime Packager，您可以封裝特定DRM解決方案或多個DRM解決方案的內容。

   下列範例指令顯示不同DRM解決方案封裝內容的一些範例：

   * [Widevine搭配Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19) （產生MPD檔案）：

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

   * [FairPlay與Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) （產生M3U8檔案）：

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
      >此 `key_url` 值會依原樣複製到M3U8檔案中。

1. 建立「店面伺服器」。

       店面伺服器需要處理下列作業：
   
   1. 客戶選擇內容。 此實作需要包含端點，以便使用者端請求特定內容ID的內容權杖。
   1. 客戶權益
   1. 來自使用者端的授權權杖(ExpressPlay)請求( [ExpressPlay授權權杖請求/回應參考](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. 建立您的使用者端。

       使用者端應包含對您的店面伺服器的呼叫。 Adobe建議使用者端在使用者選取部分內容後，以及在使用者通過驗證後，呼叫店面。 然後，將從ExpressPlay傳回的Token傳遞至您的播放器，以用於授權請求。 以下是有關實作播放器DRM元件的簡介：
   
   * [HTML5的瀏覽器TVSDK](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 有了授權權杖，使用者端現在可以從權杖衍生請求URL，向ExpressPlay提出授權請求，然後為使用者播放選取的內容。
