---
description: TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關操作，例如當新的DRM中繼資料可用時。
title: DRM事件
exl-id: 8a3bd8c7-1e76-4d26-8f88-e29eb0a0e1b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關操作，例如當新的DRM中繼資料可用時。

若要收到有關所有DRM相關事件的通知，請註冊實作 `MediaPlayer.DRMEventListener` 包含下列回呼。

| 事件 | 含義 |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | 有新的DRM中繼資料可供使用。 |
