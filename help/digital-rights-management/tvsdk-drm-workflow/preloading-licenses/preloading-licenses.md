---
title: 離線播放的預載授權概觀
description: 離線播放的預載授權概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# 預載離線播放的授權{#pre-loading-licenses-for-offline-playback}

您可以預先載入播放受Primetime DRM保護的內容所需的授權。 預先載入的授權可讓使用者檢視內容，不論他們是否有作用中的網際網路連線。

預先載入程式本身&#x200B;*需要使用網際網路連線。*&#x200B;您可以提前使用`DRMManager.loadVoucher()`來預先載入授權。 之後，當客戶希望播放所要的內容時，DRM系統已經預先預先預先，並且可以立即播放受保護的內容。
