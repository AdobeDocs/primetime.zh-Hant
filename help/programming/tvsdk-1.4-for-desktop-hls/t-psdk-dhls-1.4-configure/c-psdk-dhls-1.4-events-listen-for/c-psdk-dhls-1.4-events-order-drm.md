---
description: TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關作業，例如當新的DRM中繼資料可用時。 您的播放器可以實施動作來回應這些事件。
title: DRM事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關作業，例如當新的DRM中繼資料可用時。 您的播放器可以實施動作來回應這些事件。

若要收到有關所有DRM相關事件的通知，請聆聽下列內容：

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

下列範例顯示典型的進度：

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```
