---
description: Flash運行時TVSDK需要一個簽名令牌來驗證您有權在應用程式所在的域上調用TVSDK API。
title: 載入簽名標籤
exl-id: fef6b764-dc65-412e-a990-3f0b1fef94dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 載入簽名標籤 {#load-your-signed-token}

Flash運行時TVSDK需要一個簽名令牌來驗證您有權在應用程式所在的域上調用TVSDK API。

1. 從您的Adobe代表處獲取每個域的簽名令牌（其中每個域可以是特定域或通配符域）。

       要獲取令牌，請提供與儲存或載入應用程式的域的Adobe，或者，最好將域作為SHA256哈希。 作為回報，Adobe為每個域提供簽名令牌。 這些令牌採用以下形式之一：
   
   * 安 [!DNL .xml] 用作單個域或通配符域的標籤的檔案。

      >[!NOTE]
      >
      >通配符域的令牌覆蓋該域及其所有子域。 例如，域的通配符標籤 [!DNL mycompany.com] 也可以 [!DNL vids.mycompany.com] 和 [!DNL private.vids.mycompany.com];用於 [!DNL vids.mycompany.com] 也可以 [!DNL private.vids.mycompany.com]。 *只有某些Flash Player版本才支援通配符域令牌。*

   * A [!DNL .swf] 包含多個域（不包括通配符）（單個或通配符）的令牌資訊的檔案，您的應用程式可以動態載入這些資訊。

1. 將令牌檔案儲存在與應用程式相同的位置或域中。

   預設情況下，TVSDK在此位置中查找令牌。 或者，可以在中指定標籤的名稱和位置 `flash_vars` 你的HTML檔案。
1. 如果令牌檔案是單個XML檔案：
   1. 使用 `utils.AuthorizedFeaturesHelper.loadFrom` 下載儲存在指定URL（令牌檔案）上的資料，並提取 `authorizedFeatures` 資訊。

      此步驟可能有所不同。 例如，您可能希望在啟動應用程式之前執行身份驗證，或者您可能直接從內容管理系統(CMS)接收令牌。

   1. TVSDK派單 `COMPLETED` 事件 `FAILED` 事件。 在檢測到任一事件時採取適當的操作。

      這必須成功，您的應用程式才能提供所需 `authorizedFeatures` 對象以TVSDK的形式 `MediaPlayerContext`。
   此示例說明如何使用單令牌 [!DNL .xml] 的子菜單。

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

1. 如果令牌是 [!DNL .swf] 檔案：
   1. 定義 `Loader` 類以動態載入 [!DNL .swf] 的子菜單。
   1. 設定 `LoaderContext` 指定當前應用程式域中的載入，這允許TVSDK在 [!DNL .swf] 的子菜單。 如果 `LoaderContext` 未指定，預設操作為 `Loader.load` 是在當前域的子域中載入.swf。
   1. 偵聽COMPLETE事件，如果載入成功，TVSDK將調度該事件。

      還要偵聽ERROR事件並採取相應的操作。
   1. 如果載入成功，請使用 `AuthorizedFeaturesHelper` 去 `ByteArray` 包含PCKS-7編碼的安全資料。

      此資料通過AVE V11 API從Flash運行時播放器獲取授權確認。 如果位元組陣列沒有內容，請改用該過程查找單域令牌檔案。
   1. 使用 `AuthorizedFeatureHelper.loadFeatureFromData` 從位元組陣列獲取所需資料。
   1. 卸載 [!DNL .swf] 的子菜單。

   以下示例說明如何使用多令牌 [!DNL .swf] 的子菜單。

   **多標籤示例1:**

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

   **多令牌示例2:**

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
