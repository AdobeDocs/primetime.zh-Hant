---
title: 封鎖限制存取受保護內容的應用程式執行階段清單
description: 封鎖限制存取受保護內容的應用程式執行階段清單
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 封鎖限制存取受保護內容的應用程式執行階段清單 {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

指定無法存取內容的Primetime或Flash執行階段版本。 指定限制的執行階段(Flash Player、AIR或iOS)、平台和版本。

使用案例範例：類似DRM使用者端封鎖清單，可將最新版本的Flash Player、AIR或iOS執行階段指定為授權取得和內容播放所需的最低版本。

除了下列屬性外，應用程式執行階段還可由DRM使用者端版本支援的任何屬性來識別：

| **屬性** | **支援的值** | **符合條件** | **說明** |
|---|---|---|---|
| 應用 | 「FlashPlayer」、「AIR」、「DRM_Library」、「AVE」 | 完全相符 | 識別應用程式執行階段的名稱。 |
