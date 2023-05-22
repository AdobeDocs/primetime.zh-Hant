---
title: 標準AAXS DRM工作流
description: 標準AAXS DRM工作流
exl-id: 3bc6aa6a-cda6-4c83-af08-f27eb103a47a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 標準AAXS DRM工作流{#standard-aaxs-drm-workflow}

1. （包）AAXS Java SDK生成隨機CEK。
1. （包）CEK用於加密內容。
1. （包）CEK使用AAXS許可證伺服器的公鑰進行加密。
1. （包）加密的CEK被插入內容的DRM元資料中。
1. 該設備嘗試通過從AAXS伺服器請求許可來播放內容。
1. （授權）AAXS伺服器使用其私鑰從元資料中解密CEK。
1. （授權）AAXS伺服器向設備發出包含CEK的許可證。
