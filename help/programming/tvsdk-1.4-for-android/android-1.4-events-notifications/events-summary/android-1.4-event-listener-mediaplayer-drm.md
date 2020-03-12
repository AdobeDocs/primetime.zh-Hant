---
description: TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。
seo-description: TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。
seo-title: DRM事件
title: DRM事件
uuid: c4d96e06-2268-4e38-9d05-68ccbe912484
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# DRM事件{#drm-events}

TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。

若要收到所有DRM相關事件的通知，請註冊包含下 `MediaPlayer.DRMEventListener` 列回呼的實作。

| 事件 | 意義 |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo))`(DRMMetadataInfo drmMetadataInfo)` | 有新的DRM中繼資料可供使用。 |

