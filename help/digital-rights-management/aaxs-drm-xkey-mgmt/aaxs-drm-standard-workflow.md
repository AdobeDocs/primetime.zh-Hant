---
title: 標準AAXS DRM工作流程
description: 標準AAXS DRM工作流程
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 標準AAXS DRM工作流程{#standard-aaxs-drm-workflow}

1. （套件） AAXS Java SDK產生隨機CEK。
1. （封裝） CEK會用於加密內容。
1. （套件） CEK已使用AAXS License Server的公開金鑰加密。
1. （封裝）加密的CEK會插入內容的DRM中繼資料中。
1. 裝置會向AAXS伺服器請求授權，以嘗試播放內容。
1. （授權） AAXS伺服器會使用其私密金鑰，從中繼資料解密CEK。
1. （授權） AAXS伺服器會向裝置發出包含CEK的授權。
