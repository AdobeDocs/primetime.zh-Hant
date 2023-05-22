---
title: 維護受信任內容包器的允許清單
description: 維護受信任內容包器的允許清單
copied-description: true
exl-id: 4c296d23-75c1-4d0b-a636-31b49e99c753
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# 維護受信任內容包器的允許清單 {#maintain-a-allowlist-of-trusted-content-packagers}

安 **允許清單** 是受信任實體的清單。 在內容打包器的情況下，這些是內容所有者信任的組織來打包（或加密）FLV/F4V視頻檔案，從而建立受DRM保護的內容。 在部署Adobe訪問時，建議您維護受信任內容包的允許清單，並在頒發許可證之前驗證受DRM保護檔案的DRM元資料（DRM頭）中包含的內容包的標識。

要瞭解有關獲取有關打包內容的實體的資訊的詳細資訊，請參見 `V2ContentMetaData.getPackagerInfo()` 的 *Adobe訪問API參考*。
