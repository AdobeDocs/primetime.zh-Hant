---
title: 客戶端上的黃金時段DRM
description: 客戶端上的黃金時段DRM
copied-description: true
exl-id: 157d558f-3014-4d05-bba1-e73134cedc23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 客戶端上的黃金時段DRM{#primetime-drm-on-the-client}

播放受保護內容的黃金時段TVSDK應用程式必須首先調用黃金時段DRM API以啟動用於許可證消耗和保護內容回放的工作流。 在該工作流中，客戶端上的黃金時段DRM從受保護內容的元資料構造許可請求，然後將其發送到黃金時段DRM許可伺服器。

在發出許可請求之前，客戶端可以選擇執行必要的驗證/授權（取決於您的業務規則）。
