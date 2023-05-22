---
description: 允許清單是受信任實體的清單。
title: 維護受信任內容包器的允許清單
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 維護受信任內容包器的允許清單 {#maintain-a-allowlist-of-trusted-content-packagers}

允許清單是受信任實體的清單。

對於內容打包器，實體是內容所有者信任的組織，可以打包（或加密）視頻檔案並建立受DRM保護的內容。 部署Adobe PrimetimeDRM時，應維護受信任內容包的允許清單。 在頒發許可證之前，還必須驗證受DRM保護檔案的DRM元資料中內容打包器的身份。

要瞭解如何獲取有關打包內容的實體的資訊，請參見 [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())。
