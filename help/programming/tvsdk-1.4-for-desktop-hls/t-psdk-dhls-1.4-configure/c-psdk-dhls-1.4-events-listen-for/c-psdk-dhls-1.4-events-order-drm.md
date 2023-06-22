---
description: TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關操作，例如當新的DRM中繼資料可用時。 您的播放器可以實作動作來回應這些事件。
title: DRM事件
exl-id: 712347f3-f103-4c08-ad19-af1dd59ac549
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關操作，例如當新的DRM中繼資料可用時。 您的播放器可以實作動作來回應這些事件。

若要收到有關所有DRM相關事件的通知，請監聽以下內容：

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

下列範例顯示典型的行進：

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```
