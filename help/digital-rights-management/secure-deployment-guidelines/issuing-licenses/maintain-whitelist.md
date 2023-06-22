---
description: 允許清單是受信任實體的清單。
title: 維護受信任內容封裝者的允許清單
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 維護受信任內容封裝者的允許清單 {#maintain-a-allowlist-of-trusted-content-packagers}

允許清單是受信任實體的清單。

對於內容封裝者而言，實體是內容擁有者信任用來封裝（或加密）視訊檔案並建立受DRM保護內容的組織。 部署Adobe Primetime DRM時，您應保留受信任內容封裝器的允許清單。 您還必須先在受DRM保護的檔案的DRM中繼資料中驗證內容封裝者的身份，然後再簽發授權。

若要瞭解如何取得封裝內容的實體相關資訊，請參閱 [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
