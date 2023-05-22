---
description: TVSDK響應於諸如當新的DRM元資料變為可用時的DRM相關操作而調度數字權限管理(DRM)事件。
title: DRM事件
exl-id: 65a02744-8973-418d-9a9c-53a2a313f631
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# DRM事件{#drm-events}

TVSDK響應於諸如當新的DRM元資料變為可用時的DRM相關操作而調度數字權限管理(DRM)事件。

要獲知所有與DRM相關的事件，請收聽 `DRMMetadataInfoEvent` 用於DRM事件 `MediaPlayer` 的雙曲餘切值。

| 事件 | 意義 |
|---|---|
| DRMMetadataInfoEvent。[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 新DRM元資料可用。 |
