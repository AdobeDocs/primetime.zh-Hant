---
description: TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關操作，例如當新的DRM中繼資料可用時。
title: DRM事件
exl-id: 65a02744-8973-418d-9a9c-53a2a313f631
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關操作，例如當新的DRM中繼資料可用時。

若要收到有關所有DRM相關事件的通知，請接聽 `DRMMetadataInfoEvent` 對於具有的DRM事件 `MediaPlayer` 物件。

| 事件 | 含義 |
|---|---|
| DRMMetadataInfoEvent。[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 有新的DRM中繼資料可供使用。 |
