---
description: TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。
title: DRM事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# DRM事件{#drm-events}

TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。

要獲得所有與DRM相關的事件的通知，請註冊包含以下回呼的`MediaPlayer.DRMEventListener`實作。

| 事件 | 意義 |
|---|---|
| [onDRMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | 有新的DRM中繼資料可供使用。 |

