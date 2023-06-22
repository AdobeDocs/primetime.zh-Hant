---
description: 您可以使用ExpressPlay的Bento4封裝程式，為Primetime Cloud DRM支援的任何DRM解決方案準備內容（由ExpressPlay提供技術支援）。
title: ExpressPlay Packager / Cloud DRM / TVSDK
exl-id: ff937279-3866-4d0a-9a19-cf61726299e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

您可以使用ExpressPlay的Bento4封裝程式，為Primetime Cloud DRM支援的任何DRM解決方案準備內容（由ExpressPlay提供技術支援）。

本任務說明如何使用第三方工具來準備受保護的內容，本例中為 *ExpressPlay Bento4工具*，用於各種DRM解決方案。 如需詳細資訊，請參閱 *Bento4工具* 相關檔案： [ExpressPlay](https://www.expressplay.com/developer/) 網站。
1. 取得ExpressPlay帳戶並取得您的ExpressPlay客戶驗證程式資訊。

   另請參閱 [Primetime DRM雲端快速入門。](../../quick-start/quick-overview.md)
1. 如果您正在加密Primetime存取的內容，請從Adobe取得PrimetimeAdobe存取SDK，以及必要的憑證（授權、傳輸和封裝憑證）。
1. 提供內容加密金鑰(CEK)和內容加密金鑰儲存ID (CEKSID)，以用於DRM系統。 （您使用OpenSSL或類似工具隨機產生這些連結。）

   CEK是您用來加密視訊檔案的實際金鑰。 您可以將其安全地儲存在您自己的金鑰管理系統中的伺服器上，也可以使用ExpressPlay的 [金鑰儲存解決方案](https://www.expressplay.com/developer/key-storage/).

   CEKSID是特定CEK的識別碼。 您（通常）不會傳遞加密金鑰。 例如，請求授權權杖時，您會提供CEKSID。

1. 如果您正在加密內容以存取，請利用您的CEK建立與內容相關聯的Primetime Access中繼資料。

1. 將您的內容片段，以便為 *Bento4 MP4DASH* 工具。

   對於此步驟，您可以使用 *MP4FRAGMENT* 工具。 您只需要將內容片段化一次。 例如：

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. 使用 *Bento4 MPDASH* 「破折號」並加密零碎內容的工具。

   使用此指令來指定您將使用的所有DRM系統，並傳入從先前步驟產生的任何Primetime存取中繼資料。 例如：

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

       此伺服器需要處理下列作業：
   
   1. 客戶選擇內容。 此實作需要包含端點，以便使用者端請求特定內容ID的內容權杖。
   1. 客戶權益
   1. 來自使用者端的授權權杖(ExpressPlay)請求( [ExpressPlay授權權杖請求/回應參考](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. 建立您的使用者端。

   使用者端應包含對您的店面伺服器的呼叫。 Adobe建議使用者端在使用者選取部分內容後，以及在使用者通過驗證後，呼叫店面。 然後，將從ExpressPlay傳回的Token傳遞至您的播放器，以用於授權請求。 以下是有關實作播放器DRM元件的簡介：

   * HTML5的瀏覽器TVSDK
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 有了授權權杖，使用者端現在可以從權杖衍生請求URL，向ExpressPlay提出授權請求，然後播放使用者選取的受保護內容。
