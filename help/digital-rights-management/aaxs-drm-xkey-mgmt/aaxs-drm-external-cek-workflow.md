---
title: AAXS DRM外部CEK工作流程
description: 此工作流程與大部分現有的DRM系統不同，因為它不需要使用任何中央儲存庫或內容金鑰管理系統(CKMS)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# AAXS DRM外部CEK工作流程{#aaxs-drm-external-cek-workflow}

此工作流程與大部分現有的DRM系統不同，因為它不需要使用任何中央儲存庫或內容金鑰管理系統(CKMS)。 然而，對於希望AAXS能搭配其現有CKMS使用的客戶，AAXS提供了「外部CEK」功能，其中CEK是在封裝和授權簽發時由外部提供。

![](assets/ECEK_Workflow.PNG)

1. （套件） AAXS Java SDK提供CEK和CEK ID。
1. （封裝） CEK會用於加密內容。
1. （封裝） CEK ID會插入內容的DRM中繼資料中。
1. 裝置會向AAXS伺服器請求授權，以嘗試播放內容。
1. （授權） AAXS伺服器會從內容中繼資料中擷取CEK ID。
1. AAXS伺服器會從CKMS擷取CEK。
1. （授權） AAXS伺服器會向裝置發出包含CEK的授權。
