---
description: TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。 您的播放器可以實作回應這些事件的動作。
seo-description: TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。 您的播放器可以實作回應這些事件的動作。
seo-title: DRM事件
title: DRM事件
uuid: 729fe524-1047-4188-b4e6-96bfc5af4ae0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# DRM事件{#drm-events}

TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。 您的播放器可以實作回應這些事件的動作。

要獲得所有與DRM相關的事件的通知，請監聽以下內容：

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

以下示例顯示典型的進度：

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```

