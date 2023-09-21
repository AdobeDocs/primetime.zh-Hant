---
description: 您可以完成Digital Rights Management(DRM)特定的工作流程。
title: Digital Rights Management
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Digital Rights Management {#digital-rights-management}

您可以完成Digital Rights Management(DRM)特定的工作流程。

您可以聆聽 `AdobePSDK.DRMMetadataInfoEvent` 處理DRM工作流程的事件：

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## 新增Digital Rights Management {#add-digital-rights-management}

1. 新增 `DRMMetadataInfoAvailableEvent` 以取得 `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. 實作 `onDRMMetadataInfoAvailable` 區段在步驟1的行上方。

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

1. 以setupVideo方法建立DRMManager。

   ```js
   var drmManager = player.drmManager;
   ```

1. 複製下列範例來建立Widevine和PlayReady的保護資料：

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

1. 將保護資料新增至drmManager。

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. 將資源URL變更為DASH測試資料流。

   >[!TIP]
   >
   >請確定您更新資源型別，因為現在是DASH。

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. 測試您的設定。
