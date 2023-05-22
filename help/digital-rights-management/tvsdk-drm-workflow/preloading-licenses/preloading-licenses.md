---
title: 預載入許可證以用於離線播放概述
description: 預載入許可證以用於離線播放概述
copied-description: true
exl-id: 0d49c0e4-821b-4354-b92d-bbe2c07e467b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 預載入用於離線播放的許可證 {#pre-loading-licenses-for-offline-playback}

您可以預載入播放受Migna時DRM保護的內容所需的許可證。 預載入的許可證允許用戶查看內容，無論他們是否具有活動的Internet連接。

預載過程本身 *是* 需要Internet連接。 您可以使用 `DRMManager.loadVoucher()` 提前預載入許可證。 之後，當客戶希望播放所需內容時，DRM系統已經預先準備好，並且可以立即播放所保護的內容。
