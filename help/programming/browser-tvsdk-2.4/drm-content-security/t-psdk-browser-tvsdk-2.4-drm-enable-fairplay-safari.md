---
description: 在使用由ExpressPlay支援的Mighide DRM雲時，您可以啟用FairPlay for Safari。
title: 為Safari HLS啟用FairPlay
exl-id: 761c7cb8-3068-44c9-8ceb-6411c509c0a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 為Safari HLS啟用FairPlay {#enable-fairplay-for-safari-hls}

在使用由ExpressPlay支援的Mighide DRM雲時，您可以啟用FairPlay for Safari。

確保您具有以下功能：

* 可播放HLS視頻的正常運行的示例應用。

   該示例應用必須能夠通過ExpressPlay支援的Mogine DRM處理的授權來播放受FairPlay保護的內容。
* HLS內容示例（M3U8清單），包含FairPlay保護。

要充分利用此處的資訊，請從子部分開始瞭解多DRM工作流 [參考伺服器：示例ExpressPlay權利伺服器(SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) 中。 首先閱讀有關如何設定權利和密鑰伺服器的文檔，下面的資訊將更有用。
您需要以下項目：

* 您 *生產* 來自ExpressPlay的客戶驗證器
* 相同的內容密鑰和 `iv` 打包內容的。
* FairPlay公鑰證書的位置。

要修改FairPlay/Safari應用：

1. 設定在FairPlay許可證伺服器請求中使用的FairPlay公鑰證書的位置。

   例如：

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. 執行手動FairPlay許可證 *標籤* 請求ExpressPlay獲取許可證令牌URL。

       您可以通過以下方法之一完成此步驟：
   
   * 使用您自己的ExpressPlay生產客戶驗證器。
   * 使用相同的內容密鑰和 `iv` 在此請求中，該請求用於打包要播放的內容。

      從shell運行以下命令並替換ExpressPlay客戶驗證器以獲取示例內容的許可證令牌URL:

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      使用許可證令牌URL的響應將如下所示：

      ```
      https://fp.service.expressplay.com:80/hms/fp/rights/? 
           ExpressPlayToken=<base64-encoded ExpressPlay token>
      ```

1. 使用ExpressPlay中的許可證令牌URL設定變數。

   例如：

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. 在應用程式播放受保護的內容之前，請更改內容的URL方案 `skd://` 至 `https://`。

   在呼叫允許播放的許可證伺服器之前，您需要在應用中添加此URL方案更改。

   需要更改協定，因為提供對密鑰管理系統中內容密鑰的訪問的內容ID已打包在M3U8清單中， `skd://` 協定。 當播放器準備好獲取許可證以播放受保護的內容時，它需要首先切換協定以與ExpressPlay許可證伺服器通信。 在下面的示例中， `myServerProcessSPCPath` 修改為包含許可證伺服器請求的正確URL方案：

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
