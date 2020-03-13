---
seo-title: 內嵌授權
title: 內嵌授權
uuid: b8d8ee9b-7430-4899-9caf-47d6b64021b8
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 內嵌授權 {#embedding-licenses}

一旦內容已經加密且已預先產生授權，該授權可嵌入加密內容。

若要嵌入授權，請取得實例 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`。 如果您知道加密內容的類型，請使用或的建構 `FLVKeyMetaDataUpdater` 函式 `F4VKeyMetaDataUpdater`;否則，請 `MediaProcessorFactory.getMediaProcessor()` 使用根據檢測到的檔案類型返回實例。 建構並 `KeyMetaDataCallback` 叫用 `modifyKeyMetaData()`。 當DRM中繼資料位於加密的內容中時，將會呼叫您的回呼實作。 您可以根據找到的中繼資料，選擇要內嵌的授權，並使用 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`

如需示範內嵌授權的范常式式碼，請 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 參閱參考實作命令列工具「範例」目錄。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Adobe Access 2.0用戶端會忽略內容中內嵌的任何授權，並會嘗試從中繼資料中指定的授權伺服器取得授權。 不過，如果中繼資料指出沒有可用的授權伺服器，Adobe Access 2.0用戶端將需要升級才能檢視內容。

請 [參閱帶外授權](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md)。
