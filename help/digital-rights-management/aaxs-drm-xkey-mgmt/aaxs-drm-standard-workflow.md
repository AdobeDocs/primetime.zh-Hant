---
seo-title: 標準AAXS DRM工作流程
title: 標準AAXS DRM工作流程
description: 標準AAXS DRM工作流程
seo-description: 標準AAXS DRM工作流程
uuid: b996eb2c-8e37-4a29-a972-e09c69d2461d
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 標準AAXS DRM Workflow{#standard-aaxs-drm-workflow}

1. （封裝）AAXS Java SDK會產生隨機CEK。
1. （封裝）CEK用於加密內容。
1. （封裝）CEK會使用AAXS授權伺服器的公開金鑰加密。
1. （封裝）加密的CEK被插入內容的DRM元資料中。
1. 裝置會嘗試從AAXS伺服器要求授權來播放內容。
1. （授權）AAXS伺服器使用其私密金鑰從中繼資料解密CEK。
1. （授權）AAXS伺服器會向裝置發出包含CEK的授權。
