---
description: 您可以使用Adobe的離線打包器為由ExpressPlay支援的Mogine Cloud DRM支援的任何DRM解決方案準備內容。
title: 黃金時段打包器/雲DRM/TVSDK
exl-id: 2055c18b-62de-41bf-9644-f366609e0198
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# 黃金時段打包器/雲DRM/TVSDK {#primetime-packager-cloud-drm-tvsdk}

您可以使用Adobe的離線打包器為由ExpressPlay支援的Mogine Cloud DRM支援的任何DRM解決方案準備內容。

這組說明假定您已經設定了ExpressPlay管理帳戶： [黃金時段DRM雲快速啟動](../../../multi-drm-workflows/quick-start/quick-overview.md)。
1. 選擇用於打包內容的基礎架構。 Mighine Packager支援基於命令行和基於配置的內容打包，以便與FairPlay、Widevine和PlayReady DRM一起使用。 TVSDK當前支援以下格式和加密（管道中包含更多格式）:

   * DASH(CENC)/PlayReady, Widevine — 用於HTML5
   * HLS/FairPlay, Access — 用於iOS

1. 選擇密鑰管理系統(KMS):

   * 使用ExpressPlay的KMS( [ExpressPlay密鑰儲存](https://www.expressplay.com/developer/key-storage/));此系統通過ExpressPlay的REST風格API管理您的內容密鑰。

      或……

   * 設定您自己的KMS 建立內容鍵的資料庫，可按Content-ID選擇。

      在兩種情況下，KMS都管理內容密鑰的供應，每個密鑰都具有關聯的內容ID。

1. 打包您的內容。 使用Mighide Packager ，您可以為特定DRM解決方案或多個DRM解決方案打包一段內容。

   以下示例命令顯示了為不同DRM解決方案打包內容的一些示例：

   * [Widevine與黃金時段打包器](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19) （生成MPD檔案）:

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

   * [FairPlay與黃金時段打包器](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) （生成M3U8檔案）:

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
      >的 `key_url` 值按M3U8檔案中的方式複製。

1. 建立「店面伺服器」。

       店面伺服器需要處理以下操作：
   
   1. 客戶選擇內容。 此實現需要包括客戶端請求特定內容ID的內容令牌的終結點。
   1. 客戶權利
   1. 來自客戶端的許可證令牌(ExpressPlay)請求( [ExpressPlay許可證令牌請求/響應引用](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. 建立客戶端。

       客戶端應包括對您的店面伺服器的呼叫。 Adobe建議用戶在選擇某些內容後，在用戶經過身份驗證後，客戶端調用店面。 然後，將從ExpressPlay返回的令牌傳遞給您的播放器以用於許可證請求。 要實施玩家的DRM元件，請參閱：
   
   * [用於HTML5的瀏覽器TVSDK](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 隨著許可證令牌的手持，客戶機現在可以從令牌中導出請求URL並向ExpressPlay發出許可證請求，然後為用戶播放所選內容。
