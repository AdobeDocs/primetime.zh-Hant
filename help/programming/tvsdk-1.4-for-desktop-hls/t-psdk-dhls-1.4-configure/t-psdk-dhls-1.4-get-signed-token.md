---
description: Flash執行階段TVSDK需要有簽名的Token，以驗證您有權在應用程式所在的網域上呼叫TVSDK API。
title: 載入您的已簽署Token
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# 載入您的已簽署Token {#load-your-signed-token}

Flash執行階段TVSDK需要有簽名的Token，以驗證您有權在應用程式所在的網域上呼叫TVSDK API。

1. 從您的Adobe代表取得每個網域的簽名Token（其中每個網域可以是特定網域或萬用字元網域）。

       若要取得Token，請提供Adobe以儲存或載入您應用程式的網域，或以SHA256雜湊的形式提供網域。作為回報，Adobe會為您提供每個網域的已簽署Token。 這些預付碼採用下列其中一種形式：
   
   * [!DNL .xml]檔案，用作單一網域或萬用字元網域的Token。

      >[!NOTE]
      >
      >萬用字元網域的Token涵蓋該網域及其所有子網域。 例如，域[!DNL mycompany.com]的萬用字元也會涵蓋[!DNL vids.mycompany.com]和[!DNL private.vids.mycompany.com];[!DNL vids.mycompany.com]的萬用字元也會涵蓋[!DNL private.vids.mycompany.com]。 *只有某些Flash Player版本才支援萬用字元網域Token。*

   * [!DNL .swf]檔案，包含多個網域的Token資訊（不包括萬用字元）（單一或萬用字元），您的應用程式可動態載入。

1. 將Token檔案儲存在與應用程式相同的位置或網域中。

   依預設，TVSDK會在此位置尋找代號。 或者，您也可以在HTML檔案的`flash_vars`中指定Token的名稱和位置。
1. 如果您的Token檔案是單一XML檔案：
   1. 使用`utils.AuthorizedFeaturesHelper.loadFrom`下載儲存在指定URL（Token檔案）的資料，並從中擷取`authorizedFeatures`資訊。

      這個步驟可能有所不同。 例如，您可能想在啟動應用程式之前先執行驗證，或直接從您的內容管理系統(CMS)接收Token。

   1. 如果載入成功，TVSDK將調度`COMPLETED`事件，否則調度`FAILED`事件。 偵測到任一事件時，請採取適當的動作。

      這必須成功，您的應用程式才能以`MediaPlayerContext`的形式，將必要的`authorizedFeatures`物件提供給TVSDK。
   此範例說明如何使用單一Token [!DNL .xml]檔案。

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

1. 如果您的Token是[!DNL .swf]檔案：
   1. 定義`Loader`類別，以動態載入[!DNL .swf]檔案。
   1. 設定`LoaderContext`以指定載入在目前應用程式網域中，讓TVSDK在[!DNL .swf]檔案中選擇正確的Token。 如果未指定`LoaderContext`，則`Loader.load`的預設動作是在目前網域的子網域中載入。swf。
   1. 請監聽COMPLETE事件，如果載入成功，TVSDK會調度該事件。

      此外，還監聽ERROR事件並採取適當的操作。
   1. 如果載入成功，請使用`AuthorizedFeaturesHelper`獲取包含PCKS-7編碼安全資料的`ByteArray`。

      此資料會透過AVE V11 API使用，以從Flash執行階段播放器取得授權確認。 如果位元組陣列沒有內容，請改用程式來尋找單網域Token檔案。
   1. 使用`AuthorizedFeatureHelper.loadFeatureFromData`從位元組陣列獲取所需資料。
   1. 卸載[!DNL .swf]檔案。

   下列範例說明如何使用多Token [!DNL .swf]檔案。

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

