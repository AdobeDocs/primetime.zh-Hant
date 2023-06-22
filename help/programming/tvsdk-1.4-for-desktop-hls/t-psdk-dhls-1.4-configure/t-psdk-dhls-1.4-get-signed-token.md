---
description: Flash執行階段TVSDK需要簽署的權杖，以驗證您是否有權利在應用程式所在的網域上呼叫TVSDK API。
title: 載入您的簽署Token
exl-id: fef6b764-dc65-412e-a990-3f0b1fef94dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 載入您的簽署Token {#load-your-signed-token}

Flash執行階段TVSDK需要簽署的權杖，以驗證您是否有權利在應用程式所在的網域上呼叫TVSDK API。

1. 向您的Adobe代表取得每個網域的簽署權杖（其中每個網域可能是特定網域或萬用字元網域）。

       若要取得Token，請為Adobe提供將儲存或載入您的應用程式的網域，或最好是以SHA256雜湊形式提供網域。 作為回報，Adobe會為您提供每個網域的已簽署Token。 這些Token採用下列其中一種形式：
   
   * 一個 [!DNL .xml] 做為單一網域或萬用字元網域之權杖的檔案。

      >[!NOTE]
      >
      >萬用字元網域的代號涵蓋該網域及其所有子網域。 例如，網域的萬用字元權杖 [!DNL mycompany.com] 也會涵蓋 [!DNL vids.mycompany.com] 和 [!DNL private.vids.mycompany.com]；的萬用字元權杖 [!DNL vids.mycompany.com] 也會涵蓋 [!DNL private.vids.mycompany.com]. *僅特定Flash Player版本支援萬用字元網域權杖。*

   * A [!DNL .swf] 包含多個網域（不包括萬用字元） （單一或萬用字元）的權杖資訊的檔案，您的應用程式可動態載入。

1. 將權杖檔案儲存在與應用程式相同的位置或網域中。

   根據預設，TVSDK會在此位置尋找權杖。 或者，您也可以在「 」中指定權杖的名稱和位置 `flash_vars` 在您的HTML檔案中。
1. 如果您的Token檔案是單一XML檔案：
   1. 使用 `utils.AuthorizedFeaturesHelper.loadFrom` 以下載儲存在指定URL的資料（權杖檔案）並解壓縮 `authorizedFeatures` 其中的資訊。

      此步驟可能有所不同。 例如，您可能想要在啟動應用程式之前執行驗證，或者您可能直接從內容管理系統(CMS)接收權杖。

   1. TVSDK會傳送 `COMPLETED` 事件(如果載入成功或 `FAILED` 事件（否則）。 偵測到任一事件時，請採取適當動作。

      這必須成功，您的應用程式才能提供必要的 `authorizedFeatures` TVSDK的物件，格式為 `MediaPlayerContext`.
   此範例說明如何使用單一權杖 [!DNL .xml] 檔案。

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

1. 如果您的權杖為 [!DNL .swf] 檔案：
   1. 定義 `Loader` 類別以動態載入 [!DNL .swf] 檔案。
   1. 設定 `LoaderContext` 以指定載入位在目前應用程式網域中，如此可讓TVSDK在 [!DNL .swf] 檔案。 若 `LoaderContext` 未指定，預設動作為 `Loader.load` 是在目前網域的子網域中載入.swf。
   1. 接聽COMPLETE事件，如果載入成功，TVSDK就會傳送該事件。

      同時接聽ERROR事件並採取適當的動作。
   1. 如果載入成功，請使用 `AuthorizedFeaturesHelper` 以取得 `ByteArray` 其中包含PCKS-7編碼的安全性資料。

      此資料會透過AVE V11 API用來從Flash執行階段播放器取得授權確認。 如果位元組陣列沒有內容，請改用程式來尋找單一網域權杖檔案。
   1. 使用 `AuthorizedFeatureHelper.loadFeatureFromData` 以從位元組陣列取得所需的資料。
   1. 解除安裝 [!DNL .swf] 檔案。

   以下範例說明如何使用多權杖 [!DNL .swf] 檔案。

   **多語彙基元範例1：**

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

   **多語彙基元範例2：**

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
