---
title: 預先載入離線播放的授權概述
description: 預先載入離線播放的授權概述
copied-description: true
exl-id: 0d49c0e4-821b-4354-b92d-bbe2c07e467b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 預先載入離線播放的授權 {#pre-loading-licenses-for-offline-playback}

您可以預先載入播放受Primetime DRM保護的內容所需的授權。 預先載入的授權可讓使用者檢視內容，無論他們是否有使用中的網際網路連線。

預先載入程式本身 *會* 需要網際網路連線。 您可以使用 `DRMManager.loadVoucher()` 提前預先載入授權。 之後，當使用者端希望播放所需內容時，DRM系統已預先準備好，可以立即播放受保護的內容。
