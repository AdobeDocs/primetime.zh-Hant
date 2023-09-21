---
title: 使用者端上的Primetime DRM
description: 使用者端上的Primetime DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 使用者端上的Primetime DRM{#primetime-drm-on-the-client}

播放受保護內容的Primetime TVSDK應用程式必須先呼叫Primetime DRM API，以起始授權消耗和受保護內容播放的工作流程。 在此工作流程中，使用者端上的Primetime DRM會從受保護內容的中繼資料建構授權請求，然後將其傳送至Primetime DRM授權伺服器。

在發出授權要求之前，使用者端可選擇執行必要的驗證/授權（視您的商業規則而定）。
