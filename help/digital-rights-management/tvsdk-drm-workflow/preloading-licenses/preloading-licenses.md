---
seo-title: 離線播放的預載授權概觀
title: 離線播放的預載授權概觀
uuid: 71e5169b-7f70-4723-9f9b-fdff822c5876
translation-type: tm+mt
source-git-commit: 9bbcb228d3367fbf53de811bf2941ca653ce3b0e

---


# 預先載入授權以進行離線播放 {#pre-loading-licenses-for-offline-playback}

您可以預先載入播放受Primetime DRM保護的內容所需的授權。 預先載入的授權可讓使用者檢視內容，不論他們是否有作用中的網際網路連線。

預先載入程式本身 *需要* Internet連線。 您可以提 `DRMManager.loadVoucher()` 前使用來預先載入授權。 之後，當客戶希望播放所要的內容時，DRM系統已經預先預先預先，並且可以立即播放受保護的內容。
