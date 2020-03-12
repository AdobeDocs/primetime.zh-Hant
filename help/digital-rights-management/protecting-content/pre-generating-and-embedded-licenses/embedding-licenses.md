---
seo-title: 內嵌授權
title: 內嵌授權
uuid: e3d55376-07de-479c-9a53-04bc8071ced4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 內嵌授權 {#embedding-licenses}

一旦內容已經加密且已預先產生授權，該授權可嵌入加密內容。

如果您想要內嵌授權，則需要取得實例 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`。 如果您知道加密內容的類型，請使用或的建構 `FLVKeyMetaDataUpdater` 函式 `F4VKeyMetaDataUpdater`;否則，請 `MediaProcessorFactory.getMediaProcessor()` 使用根據檢測到的檔案類型返回實例。 然後，您需要建構並 `KeyMetaDataCallback` 叫用 `modifyKeyMetaData()`。 然後，當DRM中繼資料位於加密內容時，就會叫用您的回呼實作。 您可以根據找到的中繼資料，選擇要內嵌的授權，並使用 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`

請參 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 閱參考實作命令列工具目錄， [!DNL Samples] 以取得示範內嵌授權的范常式式碼。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Adobe Primetime DRM 2.0用戶端會忽略內嵌在內容中的任何授權，然後嘗試從中繼資料中指定的授權伺服器取得授權。 不過，如果中繼資料指出沒有可用的授權伺服器，則Primetime DRM 2.0用戶端必須先升級，您才能檢視內容。

