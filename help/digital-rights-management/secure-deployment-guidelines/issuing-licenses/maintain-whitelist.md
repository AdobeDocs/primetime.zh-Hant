---
description: 允許清單是受信任實體的清單。
seo-description: 允許清單是受信任實體的清單。
seo-title: 維護受信任內容封裝器的允許清單
title: 維護受信任內容封裝器的允許清單
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# 維護受信任內容封裝器的允許清單{#maintain-a-allowlist-of-trusted-content-packagers}

允許清單是受信任實體的清單。

對於內容封裝者，實體是受內容擁有者信任的組織，可封裝（或加密）視訊檔案並建立受DRM保護的內容。 部署Adobe Primetime DRM時，您應維護受信任內容封裝器的允許清單。 您還必須在簽發許可之前，先驗證DRM保護檔案的DRM元資料中的內容包裝器的身份。

如要瞭解如何取得有關封裝內容的實體的資訊，請參閱[V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())。
