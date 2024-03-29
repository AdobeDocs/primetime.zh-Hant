---
description: 使用Primetime DRM Cloud （採用ExpressPlay技術）時，您可以啟用適用於Safari的FairPlay。
title: 為Safari HLS啟用FairPlay
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 為Safari HLS啟用FairPlay {#enable-fairplay-for-safari-hls}

使用Primetime DRM Cloud （採用ExpressPlay技術）時，您可以啟用適用於Safari的FairPlay。

請確認您擁有下列專案：

* 可播放HLS視訊的正常運作範例應用程式。

  範例應用程式必須能夠播放受FairPlay保護的內容，並透過由ExpressPlay支援的Primetime DRM處理授權。
* 搭配FairPlay保護封裝的範例HLS內容（M3U8資訊清單）。

若要充分利用此處的資訊，請從小節開始瞭解多DRM工作流程 [參考伺服器：範例ExpressPlay軟體權利檔案伺服器(SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) 在多DRM工作流程手冊中。 首先閱讀有關如何設定權益和金鑰伺服器的檔案，以下資訊將更有用。
您需要下列專案：

* 您的 *生產* 來自ExpressPlay的客戶驗證者
* 相同的內容索引鍵和 `iv` 用於封裝內容的工具。
* 您的FairPlay公開金鑰憑證的位置。

若要修改您的FairPlay / Safari應用程式：

1. 設定FairPlay授權伺服器請求中所使用的FairPlay公開金鑰憑證的位置。

   例如：

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. 執行手動FairPlay授權 *token* 要求ExpressPlay取得授權權杖URL。

       您可以透過下列其中一種方式完成此步驟：
   
   * 使用您自己的ExpressPlay生產客戶驗證程式。
   * 使用相同的內容金鑰和 `iv` 在此要求中，用來封裝您要播放的內容。

     從殼層執行下列命令，並取代您的ExpressPlay客戶驗證器，以取得範例內容的授權權杖URL：

     ```
     curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
          customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
          errorFormat=json& 
          contentKey=<your content key>& 
          iv=<your iv here>"
     ```

     授權權杖URL的回應如下所示：

     ```
     https://fp.service.expressplay.com:80/hms/fp/rights/? 
          ExpressPlayToken=<base64-encoded ExpressPlay token>
     ```

1. 使用ExpressPlay的授權權杖URL設定變數。

   例如：

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. 在您的應用程式可播放受保護的內容之前，請先變更內容的URL配置，從 `skd://` 至 `https://`.

   呼叫允許播放的授權伺服器之前，您必須在應用程式中新增此URL配置變更。

   需要變更通訊協定，因為提供金鑰管理系統中內容金鑰存取權的內容ID會封裝在M3U8資訊清單中，並包含 `skd://` 通訊協定。 當播放器準備好取得授權以播放受保護的內容時，它需要先切換通訊協定，才能與ExpressPlay授權伺服器通訊。 在以下範例中， `myServerProcessSPCPath` 修改為包含許可證伺服器要求的正確URL配置：

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
