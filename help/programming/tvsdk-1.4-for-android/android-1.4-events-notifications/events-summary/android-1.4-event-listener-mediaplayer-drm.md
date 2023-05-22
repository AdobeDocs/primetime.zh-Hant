---
description: TVSDK響應於諸如當新的DRM元資料變為可用時的DRM相關操作而調度數字權限管理(DRM)事件。
title: DRM事件
exl-id: 8a3bd8c7-1e76-4d26-8f88-e29eb0a0e1b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK響應於諸如當新的DRM元資料變為可用時的DRM相關操作而調度數字權限管理(DRM)事件。

要獲得有關所有DRM相關事件的通知，請註冊 `MediaPlayer.DRMEventListener` 包括以下回叫。

| 事件 | 意義 |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | 新DRM元資料可用。 |
