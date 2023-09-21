---
title: 預先載入離線播放的授權概述
description: 預先載入離線播放的授權概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 預先載入離線播放的授權 {#pre-loading-licenses-for-offline-playback}

您可以預先載入播放受Primetime DRM保護的內容所需的授權。 預先載入的授權可讓使用者檢視內容，無論他們是否有使用中的網際網路連線。

預先載入程式本身 *會* 需要網際網路連線。 您可以使用 `DRMManager.loadVoucher()` 提前預先載入授權。 之後，當使用者端希望播放想要的內容時，DRM系統已預先設定好，可以立即播放受保護的內容。
