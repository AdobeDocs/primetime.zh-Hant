---
title: 阻止限制訪問受保護內容的應用程式運行時清單
description: 阻止限制訪問受保護內容的應用程式運行時清單
copied-description: true
exl-id: 7c9d9e31-1a8d-4c76-9f2c-fcda58de1a42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 阻止限制訪問受保護內容的應用程式運行時清單 {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

指定無法訪問內容的黃金時段或Flash運行時的版本。 指定受限運行時(Flash Player、AIR或iOS)、平台和版本。

示例用例：與DRM客戶端阻止清單類似，Flash Player、AIR或iOS運行時的最新版本可以指定為獲取許可證和內容回放所需的最低版本。

除了以下屬性外，應用程式運行時還可由DRM客戶端版本支援的任何屬性來標識：

| **屬性** | **支援的值** | **匹配條件** | **說明** |
|---|---|---|---|
| 應用程式 | &quot;FlashPlayer&quot;、&quot;AIR&quot;、&quot;DRM_Library&quot;、&quot;AVE&quot; | 完全匹配 | 標識應用程式運行時的名稱。 |
