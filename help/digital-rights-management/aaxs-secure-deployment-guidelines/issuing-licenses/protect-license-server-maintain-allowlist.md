---
title: 維護受信任內容封裝器的允許清單
description: 維護受信任內容封裝器的允許清單
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 維護受信任內容封裝器的允許清單{#maintain-a-allowlist-of-trusted-content-packagers}

**allow list**&#x200B;是受信任實體的清單。 在內容封裝商的情況下，這些組織是內容擁有者所信賴的組織，可封裝（或加密）FLV/F4V視訊檔案，以建立受DRM保護的內容。 部署Adobe存取時，建議您維護受信任內容封裝程式的允許清單，並且在發放授權之前，先確認DRM保護檔案的DRM中繼資料（DRM標題）中所包含的內容封裝程式的身分。

如要進一步瞭解如何取得有關封裝內容的實體的資訊，請參閱&#x200B;*Adobe存取API參考*&#x200B;中的`V2ContentMetaData.getPackagerInfo()`。
