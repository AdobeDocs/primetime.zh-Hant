---
description: TVSDK響應於諸如當新的DRM元資料變為可用時的DRM相關操作而調度數字權限管理(DRM)事件。 您的玩家可以實施響應這些事件的操作。
title: DRM事件
exl-id: 712347f3-f103-4c08-ad19-af1dd59ac549
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK響應於諸如當新的DRM元資料變為可用時的DRM相關操作而調度數字權限管理(DRM)事件。 您的玩家可以實施響應這些事件的操作。

要獲得有關所有DRM相關事件的通知，請收聽以下內容：

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

以下示例顯示了典型的晉升：

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```
