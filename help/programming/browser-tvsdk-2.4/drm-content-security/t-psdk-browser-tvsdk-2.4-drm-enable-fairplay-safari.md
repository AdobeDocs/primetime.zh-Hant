---
description: 使用Premite DRM Cloud時，您可以啟用FairPlay for Safari。
seo-description: 使用Premite DRM Cloud時，您可以啟用FairPlay for Safari。
seo-title: 為Safari HLS啟用FairPlay
title: 為Safari HLS啟用FairPlay
uuid: 6a250a31-cc4b-4c4b-b1e9-893ee3ca5d78
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 為Safari HLS啟用FairPlay {#enable-fairplay-for-safari-hls}

使用Premite DRM Cloud時，您可以啟用FairPlay for Safari。

請確定您有下列項目：

* 可播放HLS視訊的正常範例應用程式。

   範例應用程式必須能夠播放受FairPlay保護的內容，並透過由ExpressPlay提供支援的Primetime DRM處理授權。
* 使用FairPlay保護封裝的HLS內容（M3U8資訊清單）範例。

要充分利用此處的資訊，請從子部分參考伺服器開始瞭解多DRM工作 [流：Multi-DRM Workflows Guide中的ExpressPlay Entitlement Server(SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) 。 請先閱讀有關如何設定權益和金鑰伺服器的檔案，以下資訊將會更有用。
您需要下列項目：

* 您的 *ExpressPlay生產* 、客戶驗證器
* 內容金鑰與您的 `iv` 內容封裝所在位置相同。
* FairPlay公開金鑰憑證的位置。

若要修改您的FairPlay / Safari應用程式：

1. 設定FairPlay授權伺服器要求中使用之FairPlay公開金鑰憑證的位置。

   例如：

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. 對ExpressPlay執行手動FairPlay *授權Token* 要求，以取得授權Token URL。

       您可透過下列其中一種方式完成此步驟：
   
   * 使用您自己的ExpressPlay Production Customer Authenticator。
   * 請使用與此請求中 `iv` 用來封裝您要播放之內容的相同內容金鑰。

      從shell執行下列命令，並取代您的ExpressPlay客戶驗證器，以取得範例內容的授權Token URL:

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      使用授權Token URL的回應如下所示：

      ```
      https://fp.service.expressplay.com:80/hms/fp/rights/? 
           ExpressPlayToken=<base64-encoded ExpressPlay token>
      ```

1. 使用ExpressPlay的授權Token URL設定變數。

   例如：

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. 在您的應用程式播放受保護的內容之前，請先將內容的URL配置從變更 `skd://` 為 `https://`。

   您必須先在應用程式中新增此URL配置變更，才能呼叫允許播放的授權伺服器。

   必須變更通訊協定，因為提供密鑰管理系統中內容金鑰存取權的內容ID會封裝在M3U8資訊清單中，並附有通訊 `skd://` 協定。 當播放器準備好取得播放受保護內容的授權時，它需要先切換通訊協定，以便與ExpressPlay授權伺服器通訊。 在下列範例中，修改 `myServerProcessSPCPath` 為包含授權伺服器要求的正確URL配置：

   ```js
   extractContentId(initData) {  
       contentId = arrayToString(initData); // contentId is passed up as a URI,  
                                            // from which the host must be extracted:  
       var link = document.createElement('a');  
       link.href = contentId;  
       var index = contentId.indexOf(':');  
       myServerProcessSPCPath = "https:" + contentId.substring(index+1);  
       console.log("severProcessSPCPAth = " + serverProcessSPCPath); return link.hostname;  
   }
   ```

