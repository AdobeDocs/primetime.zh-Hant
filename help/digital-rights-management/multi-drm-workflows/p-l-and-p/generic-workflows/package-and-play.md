---
description: 您可以使用ExpressPlay的Bento4封裝程式，為Primetime Cloud DRM（由ExpressPlay提供）支援的任何DRM解決方案準備內容。
title: ExpressPlay Packager / Cloud DRM / TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

您可以使用ExpressPlay的Bento4封裝程式，為Primetime Cloud DRM（由ExpressPlay提供）支援的任何DRM解決方案準備內容。

本工作說明如何使用協力廠商工具來準備受保護的內容（在本例中為&#x200B;*ExpressPlay Bento4 Tools*），以便與各種DRM解決方案搭配使用。 如需詳細資訊，請參閱[ExpressPlay](https://www.expressplay.com/developer/)網站上的&#x200B;*Bento4 tools*&#x200B;說明檔案。
1. 取得ExpressPlay帳戶並取得您的ExpressPlay客戶驗證器資訊。

   請參閱[Primetime DRM Cloud快速入門。](../../quick-start/quick-overview.md)
1. 如果您要加密Primetime Access的內容，請從Adobe取得PrimetimeAdobe存取SDK，以及必要的憑證（授權、傳輸和封裝憑證）。
1. 提供內容加密密鑰(CEK)和內容加密密鑰儲存ID(CEKSID)，以用於跨DRM系統。 （您使用OpenSSL或類似程式隨機產生這些項目。）

   CEK是您用來加密視訊檔案的實際金鑰。 您可以將它安全地儲存在自己的密鑰管理系統中自己的伺服器上，也可以使用ExpressPlay的[密鑰儲存解決方案](https://www.expressplay.com/developer/key-storage/)。

   CEKSID是特定CEK的識別碼。 您（通常）不會傳遞加密金鑰。 例如，在請求授權Token時，您會提供CEKSID。

1. 如果您正在加密內容以存取，請利用您的CEK來建立與您的內容相關的Primetime Access中繼資料。

1. 將內容分段，以便為&#x200B;*Bento4 MP4DASH*&#x200B;工具準備。

   在此步驟中，您可以使用&#x200B;*MP4FRAGMENT*&#x200B;工具。 您只需要將內容分割一次。 例如：

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. 使用&#x200B;*Bento4 MPDASH*&#x200B;工具來「DASH-ify」並加密您零散的內容。

   使用此命令指定您將使用的所有DRM系統，並傳遞從前述步驟生成的任何Primetime Access元資料。 例如：

   ```
   /mp4dash -f  
   --use-segment-list  
   --use-segment-timeline  
   --encryption-key=<CEKSID>:<CEK>  
   --playready  
   --Widevine  
   --Widevine-header=provider:intertrust#content_id:2a  
   --primetime  
   --primetime-metadata=@AAXS.metadata 
    Fragmented.mp4 -o DASH_OUTPUT
   ```

1. 建立「店面伺服器」。

       此伺服器需要處理以下操作：
   
   1. 客戶選擇內容。 此實作需要包含端點，讓用戶端為特定內容ID請求內容Token。
   1. 客戶權益
   1. 來自用戶端的授權Token(ExpressPlay)要求（[ExpressPlay授權Token要求／回應參考](../../license-token-req-resp-ref/license-req-resp-overview.md)）

1. 建立您的客戶。

   客戶端應包括對店面伺服器的呼叫。 Adobe建議用戶在選擇某些內容後，以及用戶通過身份驗證後，客戶端調用店面。 然後，將從ExpressPlay傳回的Token傳遞至您的播放器，以用於授權要求。 以下是實作播放器DRM元件的簡介：

   * HTML5的瀏覽器TVSDK
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 有了授權Token，用戶端現在可以從Token衍生要求URL，並對ExpressPlay進行授權要求，然後為使用者播放選取的受保護內容。
