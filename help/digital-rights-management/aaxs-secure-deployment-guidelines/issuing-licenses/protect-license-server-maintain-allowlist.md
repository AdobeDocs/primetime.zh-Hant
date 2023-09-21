---
title: 維護受信任內容封裝者的允許清單
description: 維護受信任內容封裝者的允許清單
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# 維護受信任內容封裝者的允許清單 {#maintain-a-allowlist-of-trusted-content-packagers}

一個 **允許清單** 是受信任實體的清單。 就內容封裝者而言，這類組織是內容擁有者信任的，可封裝（或加密）FLV/F4V視訊檔案，建立受DRM保護的內容。 部署Adobe Access時，建議您維持受信任內容封裝器的允許清單，並在發行授權之前，先驗證包含在受DRM保護檔案的DRM中繼資料（DRM標頭）中的內容封裝器的身分。

若要進一步瞭解如何取得封裝內容之實體的相關資訊，請參閱 `V2ContentMetaData.getPackagerInfo()` 在 *Adobe存取API參考*.
