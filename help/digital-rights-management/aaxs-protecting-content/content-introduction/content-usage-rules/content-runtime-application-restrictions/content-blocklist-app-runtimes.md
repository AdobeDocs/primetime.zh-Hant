---
title: 封鎖應用程式執行階段清單，限制其存取受保護的內容
description: 封鎖應用程式執行階段清單，限制其存取受保護的內容
copied-description: true
exl-id: 7c9d9e31-1a8d-4c76-9f2c-fcda58de1a42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 封鎖應用程式執行階段清單，限制其存取受保護的內容 {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

指定無法存取內容的Primetime或Flash執行階段版本。 指定限制的執行階段(Flash Player、AIR或iOS)、平台和版本。

使用案例範例：類似DRM使用者端封鎖清單，可將最新版本的Flash Player、AIR或iOS執行階段指定為授權取得和內容播放所需的最低版本。

除了下列屬性外，應用程式執行階段也可以由DRM使用者端版本支援的任何屬性來識別：

| **屬性** | **支援的值** | **符合條件** | **說明** |
|---|---|---|---|
| 應用 | &quot;FlashPlayer&quot;、&quot;AIR&quot;、&quot;DRM_Library&quot;、&quot;AVE&quot; | 完全相符 | 識別應用程式執行階段的名稱。 |
