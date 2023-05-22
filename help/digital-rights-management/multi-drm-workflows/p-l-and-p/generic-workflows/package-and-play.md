---
description: 您可以使用ExpressPlay的Bento4打包程式為ExpressPlay支援的Mogine Cloud DRM支援的任何DRM解決方案準備內容。
title: ExpressPlay打包器/雲DRM/TVSDK
exl-id: ff937279-3866-4d0a-9a19-cf61726299e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# ExpressPlay打包器/雲DRM/TVSDK {#expressplay-packager-cloud-drm-tvsdk}

您可以使用ExpressPlay的Bento4打包程式為ExpressPlay支援的Mogine Cloud DRM支援的任何DRM解決方案準備內容。

此任務介紹如何使用第三方工具準備受保護的內容，在本例中 *ExpressPlay Bento4工具*，用於各種DRM解決方案。 有關其他資訊，請參閱 *Bento4工具* 文檔 [快速播放](https://www.expressplay.com/developer/) 的子菜單。
1. 獲取ExpressPlay帳戶並獲取ExpressPlay客戶驗證器資訊。

   請參閱 [黃金時段DRM雲快速啟動。](../../quick-start/quick-overview.md)
1. 如果您正在為Mighile Access加密內容，請從Adobe獲取MighileAdobe訪問SDK以及所需的證書（許可證、傳輸和打包證書）。
1. 提供內容加密密鑰(CEK)和內容加密密鑰儲存ID(CEKSID)，以在DRM系統中使用。 （您使用OpenSSL或類似程式隨機生成這些檔案。）

   CEK是您用於加密視頻檔案的實際密鑰。 您可以將它安全地儲存在您自己的密鑰管理系統中的您自己的伺服器上，或者您可以使用ExpressPlay [關鍵儲存解決方案](https://www.expressplay.com/developer/key-storage/)。

   CEKSID是特定CEK的標識符。 您（通常）不會傳遞加密密鑰。 例如，在請求許可證令牌時，提供CEKSID。

1. 如果您正在為Access加密內容，請利用您的CEK建立與您的內容關聯的Mogini時Access元資料。

1. 分段內容以準備 *本托4 MP4DASH* 工具欄。

   對於此步驟，您可以使用 *MP4片段* 工具欄。 您只需將內容分片一次。 例如：

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. 使用 *本托4 MPDASH* 工具，用於「虛線」並加密零碎內容。

   使用此命令可指定將要使用的所有DRM系統，並傳遞從前面步驟生成的任何Mogini時訪問元資料。 例如：

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
   
   1. 客戶選擇內容。 此實現需要包括客戶端請求特定內容ID的內容令牌的終結點。
   1. 客戶權利
   1. 來自客戶端的許可證令牌(ExpressPlay)請求( [ExpressPlay許可證令牌請求/響應引用](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. 建立客戶端。

   客戶端應包括對您的店面伺服器的呼叫。 Adobe建議用戶在選擇某些內容後，在用戶經過身份驗證後，客戶端調用店面。 然後，將從ExpressPlay返回的令牌傳遞給您的播放器以用於許可證請求。 要實施玩家的DRM元件，請參閱：

   * 用於HTML5的瀏覽器TVSDK
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 隨著許可證令牌的手持，客戶機現在可以從令牌中導出請求URL並向ExpressPlay發出許可證請求，然後為用戶播放所選的受保護內容。
