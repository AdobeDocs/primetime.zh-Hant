---
description: 可以完成Digital Rights Management(DRM)特定的工作流。
title: Digital Rights Management
exl-id: 5a40252b-2917-4341-bc64-8642432ddda9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Digital Rights Management {#digital-rights-management}

可以完成Digital Rights Management(DRM)特定的工作流。

你可以聽 `AdobePSDK.DRMMetadataInfoEvent` 處理DRM工作流的事件：

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## 添加Digital Rights Management {#add-digital-rights-management}

1. 添加 `DRMMetadataInfoAvailableEvent` 去 `DRMMetadata`。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. 實施 `onDRMMetadataInfoAvailable` 欄的「字型」框中的字型)的字型名稱。

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

1. 在setupVideo方法中建立DRMManager。

   ```js
   var drmManager = player.drmManager;
   ```

1. 通過複製以下示例為Widevine和PlayReady建立保護資料：

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

1. 將資源URL更改為DASHtest流。

   >[!TIP]
   >
   >請確保更新資源類型，因為現在這是DASH。

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Test配置。
