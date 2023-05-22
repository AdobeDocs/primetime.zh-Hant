---
title: AAXS DRM外部CEK工作流
description: 此工作流與大多數現有的DRM系統不同，因為它不需要使用任何中央儲存庫或內容密鑰管理系統(CKMS)
exl-id: f084aa57-8bef-40a0-b52d-4d23dfdf36c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# AAXS DRM外部CEK工作流{#aaxs-drm-external-cek-workflow}

此工作流與大多數現有的DRM系統不同，因為它不需要使用任何中央儲存庫或內容密鑰管理系統(CKMS)。 但是，對於希望AAXS與其現有CKMS協作的客戶，AAXS提供了一種稱為「外部CEK」的功能，在該功能中，CEK在打包和許可證發放時由外部提供。

![](assets/ECEK_Workflow.PNG)

1. （包）AAXS Java SDK提供CEK和CEK ID。
1. （包）CEK用於加密內容。
1. （包）將CEK ID插入內容的DRM元資料。
1. 該設備嘗試通過從AAXS伺服器請求許可來播放內容。
1. （許可）AAXS伺服器從內容元資料中提取CEK ID。
1. AAXS伺服器從CKMS中檢索CEK。
1. （授權）AAXS伺服器向設備發出包含CEK的許可證。
