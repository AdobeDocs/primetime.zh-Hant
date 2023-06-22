---
title: 維護受信任內容封裝者的允許清單
description: 維護受信任內容封裝者的允許清單
copied-description: true
exl-id: 4c296d23-75c1-4d0b-a636-31b49e99c753
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# 維護受信任內容封裝者的允許清單 {#maintain-a-allowlist-of-trusted-content-packagers}

一個 **允許清單** 是可信任實體的清單。 若是內容封裝者，這類組織是內容擁有者信任的，可封裝（或加密）FLV/F4V視訊檔案，建立受DRM保護的內容。 部署「Adobe存取」時，建議您在發行授權之前，維護一份受信任內容封裝器的允許清單，並驗證受DRM保護檔案的DRM中繼資料（DRM標頭）中所包含的內容封裝器的身分。

若要進一步瞭解如何取得封裝內容的實體相關資訊，請參閱 `V2ContentMetaData.getPackagerInfo()` 在 *Adobe存取API參考*.
