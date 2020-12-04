---
seo-title: AAXS DRM外部CEK工作流程
title: AAXS DRM外部CEK工作流程
description: 此工作流程與大多數現有的DRM系統不同，因為它不需要使用任何中央儲存庫或內容密鑰管理系統(CKMS)
seo-description: 此工作流程與大多數現有的DRM系統不同，因為它不需要使用任何中央儲存庫或內容密鑰管理系統(CKMS)
uuid: b313594b-0feb-4f27-bf02-f04b955e2140
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# AAXS DRM External CEK Workflow{#aaxs-drm-external-cek-workflow}

此工作流程與大多數現有的DRM系統不同，因為它不需要使用任何中央儲存庫或內容密鑰管理系統(CKMS)。 但是，對於希望AAXS與其現有CKMS合作的客戶，AAXS提供一種稱為「外部CEK」的功能，其中CEK在包裝和許可證發放時由外部提供。

![](assets/ECEK_Workflow.PNG)

1. （套件）AAXS Java SDK提供CEK和CEK ID。
1. （封裝）CEK用於加密內容。
1. （封裝）CEK ID會插入內容的DRM中繼資料。
1. 裝置會嘗試從AAXS伺服器要求授權來播放內容。
1. （授權）AAXS伺服器會從內容中繼資料擷取CEK ID。
1. AAXS伺服器從CKMS中檢索CEK。
1. （授權）AAXS伺服器會向裝置發出包含CEK的授權。
