---
description: 您可以根據預設解析器實作您自己的內容解析器。
seo-description: 您可以根據預設解析器實作您自己的內容解析器。
seo-title: 建置自訂內容解析程式
title: 建置自訂內容解析程式
uuid: cf85dd90-242e-4f9e-9785-158ca0fc9465
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 實作自訂內容解析器{#implement-a-custom-content-resolver}

您可以根據預設解析器實作您自己的內容解析器。

當瀏覽器TVSDK偵測到新商機時，它會重複透過已註冊的內容解析器尋找能夠使用`canResolve`方法解決該商機的內容解析器。 選擇返回true的第一個用於解決業務機會。 如果沒有內容解析程式，則會略過該商機。 由於內容解析程式通常是非同步的，因此當程式完成時，內容解析程式負責通知瀏覽器TVSDK。

請記住下列資訊：

* 內容解析器呼叫`client.process`，以指定TVSDK需要執行的時間軸作業。

   此作業通常是廣告插播位置。

* 如果解析進程成功，則內容解析器調用`client.notifyCompleted`；如果進程失敗，則調用`client.notifyFailed`。

1. 建立自訂的業務機會解析程式。

   ```js
   /** 
     * Class implementing AdobePSDK.ContentResolver interface  
   */ 
   CustomResolver = function () { 
   }; 
   
   CustomResolver.prototype = { 
       constructor: CustomResolver, 
       configureCallbackFunc: function (item, client) { 
       // here you can read any media stream characteristics which 
       // might help configure your content resolver like 
       // - the media player item configuration through the item.config 
       // - the media resource metadata through item.resource.metadata 
      }, 
   
       canResolveCallbackFunc: function (opportunity) { 
       // check if the opportunity can be resolved by this resolver 
       // if yes return true, otherwise return false 
       return true; 
      }, 
   
       resolveCallbackFunc: function (opportunity) {         
       // start the resolving process 
       // communicate with your custom ad server 
   
       // in this example we assume that: 
       // - if successful, onResolveCompleted method will be invoked 
       // - if failed, onResolveFailed method will be invoked 
      }, 
   
       onResolveCompleted: function (response) { 
        try { 
           var proposals = []; 
           // extract the timeline ad placement from the response 
           // and add them to the proposal vector 
           // - extract the ad break 
           // - calculate the placement (can reuse the _opportunity.placement) 
           // var timelineOperation = new AdobePSDK.AdBreakPlacement (adBreak, placement); 
           // proposals.push (timelineOperation); 
   
           client.process (proposals); 
           client.notifyCompleted (_opportunity); 
       } catch (error) { 
           onResolveFailed (error); 
       } 
   }, 
   
       onResolveFailed: function (error) { 
         client.notifyFailed (_opportunity); 
       } 
   
   }; 
   ```

1. 建立自訂內容工廠，使用自訂內容解析程式。

   例如：

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
       constructor: CustomContentFactory, 
       retrieveResolversCallbackFunc: function (item) { 
           var result = []; 
           var resource = item.resource; 
           if (resource.metadata.containsKey("custom-opportunity-detector")) { 
               result.push (new CustomResolver()); 
           } 
           return result; 
       }, 
       … 
   }; 
   ```

1. 註冊要播放的媒體串流的自訂內容工廠。

   在UI Framework播放器中，您可以指定自訂內容工廠，如下所示：

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var advertisingMetadata = new AdobePSDK.AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue ("customparam", "customvalue"); 
   
   var metadata = new AdobePSDK.Metadata(); 
   metadata.setMetadata ("custom-opportunity-detector", advertisingMetadata); 
   
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
       mediaPlayerItemConfig: { 
              advertisingFactory: advertisingFactory 
       }, 
          mediaResource: { 
                  resourceUrl:'Specify Resource Url', 
                  metadata: metadata 
          } 
   } 
   
   }); 
   ```

