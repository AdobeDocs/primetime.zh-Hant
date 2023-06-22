---
title: 封鎖應用程式執行階段清單
description: 封鎖應用程式執行階段清單
copied-description: true
exl-id: f8d1d385-41d4-4361-82c1-417b2ff421c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 封鎖應用程式執行階段清單 {#blocklist-of-application-runtimes}

應用程式執行階段的封鎖清單指定了無法存取內容的Primetime使用者端或Flash執行階段的版本。 指定限制的執行階段(Flash Player、AIR或iOS)、平台和版本。

使用案例範例：類似Primetime DRM使用者端封鎖清單，可將最新版本的Flash Player、AIR或iOS執行階段指定為授權取得和內容播放所需的最低版本。

除了下列屬性外，您還可以透過Primetime DRM使用者端版本支援的任何屬性來識別應用程式執行階段：

| **屬性** | **支援的值** | **符合條件** | **說明** |
|---|---|---|---|
| 應用 | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | 完全相符 | 識別應用程式執行階段的名稱。 |
