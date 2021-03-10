---
description: 您可以完成Digital Rights Management(DRM)特定的工作流程。
title: Digital Rights Management
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Digital Rights Management{#digital-rights-management}

您可以完成Digital Rights Management(DRM)特定的工作流程。

您可以監聽`AdobePSDK.DRMMetadataInfoEvent`事件以處理DRM工作流：

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## 添加Digital Rights Management{#add-digital-rights-management}

1. 新增`DRMMetadataInfoAvailableEvent`以取得`DRMMetadata`。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. 在步驟1中，實作行上方的`onDRMMetadataInfoAvailable`區段。

   ```js
   var onDRMMetadataInfoAvaialble = function(event) { 
    var drmMetadataInfo = event.drmMetadataInfo; 
    var drmMetadata = null; 
   
    if(drmMetadataInfo) { 
     drmMetadata = drmMetadataInfo.drmMetadata; 
    } 
   
    drmManager.acquireLicense(drmMetadata, null, null); 
   };
   ```

1. 在setupVideo方法中建立DRManager。

   ```js
   var drmManager = player.drmManager;
   ```

1. 通過複製以下示例，為Widevine和PlayReady建立保護資料：

   ```js
   var protectionData = { 
     "com.widevine.alpha":{ 
       "serverURL":"https://wv.service.expressplay.com/hms/wv/rights/? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]"  
     }, 
   
     "com.microsoft.playready":{ 
       "serverURL":"https://pr.test.expressplay.com/playready/RightsManager.asmx? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]", 
         "httpRequestHeaders":{ 
       } 
     } 
   };
   ```

1. 將保護資料添加到drmManager。

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. 將資源URL變更為DASH測試串流。

   >[!TIP]
   >
   >請確定您更新資源類型，因為現在是DASH。

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. 測試您的設定。