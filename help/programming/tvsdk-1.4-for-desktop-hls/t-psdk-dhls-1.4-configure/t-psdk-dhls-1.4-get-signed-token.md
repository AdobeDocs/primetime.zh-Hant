---
description: Flash Runtime TVSDK需要有簽署的Token，以驗證您有權在您應用程式所在的網域上呼叫TVSDK API。
seo-description: Flash Runtime TVSDK需要有簽署的Token，以驗證您有權在您應用程式所在的網域上呼叫TVSDK API。
seo-title: 載入您的已簽署Token
title: 載入您的已簽署Token
uuid: 8760eab3-3d6d-47c6-9aa7-f64f6aa5ddcf
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 載入您的已簽署Token {#load-your-signed-token}

Flash Runtime TVSDK需要有簽署的Token，以驗證您有權在您應用程式所在的網域上呼叫TVSDK API。

1. 請向Adobe代表取得您每個網域的簽名Token（每個網域可以是特定網域或萬用字元網域）。

       若要取得Token，請提供Adobe應用程式儲存或載入的網域，或以SHA256雜湊的形式提供網域。 作為回報，Adobe會為您提供每個網域的已簽署Token。 這些Token會採用下列其中一種形式：
   
   * 用 [!DNL .xml] 作單一網域或萬用字元網域之Token的檔案。

      >[!NOTE]
      >
      >萬用字元網域的Token涵蓋該網域及其所有子網域。 例如，網域的萬用字元也 [!DNL mycompany.com] 會涵蓋 [!DNL vids.mycompany.com] 和 [!DNL private.vids.mycompany.com];的萬用字元 [!DNL vids.mycompany.com] 也會涵蓋 [!DNL private.vids.mycompany.com]。 *只有某些Flash Player版本才支援萬用字元網域Token。*

   * 包含 [!DNL .swf] 多個網域的Token資訊（不包括萬用字元）（單一或萬用字元）的檔案，您的應用程式可動態載入此檔案。

1. 將Token檔案儲存在與應用程式相同的位置或網域中。

   依預設，TVSDK會在此位置尋找代號。 或者，您也可以在HTML檔案中指定Token的 `flash_vars` 名稱和位置。
1. 如果您的Token檔案是單一XML檔案：
   1. 使 `utils.AuthorizedFeaturesHelper.loadFrom` 用來下載儲存在指定URL（Token檔案）的資料，並從中擷 `authorizedFeatures` 取資訊。

      這個步驟可能有所不同。 例如，您可能想在啟動應用程式之前先執行驗證，或是直接從內容管理系統(CMS)接收Token。

   1. 如果載入成 `COMPLETED` 功，TVSDK會派單事件，或以其他方式 `FAILED` 派單事件。 偵測到任一事件時，請採取適當的動作。

      您的應用程式必須成功提供必要 `authorizedFeatures` 物件至TVSDK，其格式為 `MediaPlayerContext`。
   此範例說明如何使用單一Token [!DNL .xml] 檔案。

   ```
   private function loadDirectTokenURL():void { 
       var url:String = constructAuthorizedFeatureTokenURL(); 
       _logger.debug("#onApplicationComplete Loading token from [{0}].", url); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE,  
           onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR,  
           onFeatureError); 
        _authorizedFeatureHelper.loadFrom(url); 
    }
   ```

1. 如果您的Token是檔 [!DNL .swf] 案：
   1. 定義類 `Loader` 別以動態載入 [!DNL .swf] 檔案。
   1. 將設 `LoaderContext` 定為指定載入在目前應用程式網域中，讓TVSDK在檔案中選擇正確的Token [!DNL .swf] 。 如果 `LoaderContext` 未指定，預設動作 `Loader.load` 是在目前網域的子網域中載入。swf。
   1. 請監聽COMPLETE事件，如果載入成功，TVSDK會調度該事件。

      此外，還監聽ERROR事件並採取適當的操作。
   1. 如果載入成功，請使 `AuthorizedFeaturesHelper` 用獲取包 `ByteArray` 含PCKS-7編碼安全資料。

      此資料會透過AVE V11 API使用，以取得Flash Runtime Player的授權確認。 如果位元組陣列沒有內容，請改用程式來尋找單網域Token檔案。
   1. 使用 `AuthorizedFeatureHelper.loadFeatureFromData` 從位元組陣列取得所需資料。
   1. 卸載文 [!DNL .swf] 件。
   下列範例說明如何使用多重Token [!DNL .swf] 檔案。

   **多重Token範例1:**

   ```
   private function onApplicationComplete(event:FlexEvent):void { 
       var url:String = constructAuthorizedFeatureTokenURLFromSwf();   
       _loader = new Loader(); 
       var swfUrl:URLRequest = new URLRequest(url); 
       var loaderContext:LoaderContext =  
           new LoaderContext(false, ApplicationDomain.currentDomain, null); 
       _loader.contentLoaderInfo.addEventListener(Event.COMPLETE,  
           modEventHandler); 
       _loader.contentLoaderInfo.addEventListener(IOErrorEvent.IO_ERROR,  
           errEventHandler); 
       _loader.contentLoaderInfo.addEventListener(ProgressEvent.PROGRESS,  
           onProgressHandler); 
       _loader.uncaughtErrorEvents.addEventListener(UncaughtErrorEvent. 
           UNCAUGHT_ERROR, uncaughtEventHandler); 
       _logger.debug("# Loading token swf with context from [{0}].", url); 
       _loader.load(swfUrl, loaderContext); 
   } 
   
   private function modEventHandler(e:Event):void { 
       _logger.debug("loadSWF with domainID {0}",  
       SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
           loader.contentLoaderInfo.applicationDomain. 
           getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray = myTokens. 
           FetchToken(SecurityDomain.currentDomain.domainID); 
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           _logger.debug("token bytearry size {0}", byteArray.length); 
           _authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   ```

   **多重代號範例2:**

   ```
   private function tokenSwfLoadedHandler(e:Event):void { 
       trace("loadSWF with domainID {0}", SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
         loader.contentLoaderInfo.applicationDomain. 
         getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray =  
           myTokens.FetchToken(SecurityDomain.currentDomain.domainID); 
       var myDomains:Array = ["domain.com"]; 
       if (byteArray == null || byteArray.length == 0) { 
           // check for wildcard tokens 
           if (myTokens.hasOwnProperty("FetchWildCardToken") == true) { 
               // contains wildcard domains 
               for each (var domain:String in myDomains) { 
                   byteArray = myTokens.FetchWildCardToken(domain); 
                   if (byteArray != null && byteArray.length != 0) { 
                       break; 
                   } 
               }; 
           } 
       } 
   
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           trace("token bytearry size {0}", byteArray.length); 
           authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   
   private function loadDirectTokenURL():void { 
       trace("#onApplicationComplete Loading token from [{0}].", tokenUrl); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       authorizedFeatureHelper.loadFrom(tokenUrl); 
   }
   ```

