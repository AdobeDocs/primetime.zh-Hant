---
description: TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關作業，例如當新的DRM中繼資料可用時。
title: DRM事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關作業，例如當新的DRM中繼資料可用時。

若要收到有關所有DRM相關事件的通知，請接聽 `DRMMetadataInfoEvent` 對於具有的DRM事件 `MediaPlayer` 物件。

| 事件 | 含義 |
|---|---|
| DRMMetadataInfoEvent。[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 有新的DRM中繼資料可供使用。 |
