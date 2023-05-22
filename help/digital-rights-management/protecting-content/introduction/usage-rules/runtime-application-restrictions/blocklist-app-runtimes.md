---
title: 阻止應用程式運行時清單
description: 阻止應用程式運行時清單
copied-description: true
exl-id: f8d1d385-41d4-4361-82c1-417b2ff421c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 阻止應用程式運行時清單 {#blocklist-of-application-runtimes}

應用程式運行時的阻止清單指定無法訪問內容的黃金時段客戶端或Flash運行時的版本。 指定受限運行時(Flash Player、AIR或iOS)、平台和版本。

示例用例：與黃金時段DRM客戶端塊清單類似，Flash Player、AIR或iOS運行時的最新版本可以指定為許可證獲取和內容回放所需的最低版本。

除了以下屬性外，還可以通過Mogifale DRM客戶端版本支援的任何屬性來標識應用程式運行時：

| **屬性** | **支援的值** | **匹配條件** | **說明** |
|---|---|---|---|
| 應用程式 | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | 完全匹配 | 標識應用程式運行時的名稱。 |
