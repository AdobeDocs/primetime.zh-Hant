---
seo-title: 維護受信任內容封裝器的白名單
title: 維護受信任內容封裝器的白名單
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 維護受信任內容封裝器的白名單{#maintain-a-whitelist-of-trusted-content-packagers}

白 *名單* ，是受信任實體的清單。 在內容封裝商的情況下，這些組織是內容擁有者所信賴的組織，可封裝（或加密）FLV/F4V視訊檔案，以建立受DRM保護的內容。 部署Adobe Access時，建議您維護受信任內容封裝程式的白名單，並在核發授權之前，先確認DRM保護檔案的DRM中繼資料（DRM標題）中所包含的內容封裝程式的身分。

如需進一步瞭解如何取得封裝內容之實體的相關資訊，請參 `V2ContentMetaData.getPackagerInfo()` 閱 *Adobe Access API參考*。
