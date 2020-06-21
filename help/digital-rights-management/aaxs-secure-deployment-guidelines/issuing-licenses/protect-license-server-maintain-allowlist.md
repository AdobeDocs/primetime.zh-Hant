---
seo-title: 維護受信任內容封裝器的允許清單
title: 維護受信任內容封裝器的允許清單
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 維護受信任內容封裝器的允許清單{#maintain-a-allowlist-of-trusted-content-packagers}

允許 *清單* (allowlist)是受信任實體的清單。 在內容封裝商的情況下，這些組織是內容擁有者所信賴的組織，可封裝（或加密）FLV/F4V視訊檔案，以建立受DRM保護的內容。 部署Adobe Access時，建議您維護受信任內容封裝程式的允許清單，並在核發授權之前，先確認DRM保護檔案的DRM中繼資料（DRM標題）中所包含的內容封裝程式的身分。

如需進一步瞭解如何取得封裝內容之實體的相關資訊，請參 `V2ContentMetaData.getPackagerInfo()` 閱 *Adobe Access API參考*。
