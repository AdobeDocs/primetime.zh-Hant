---
seo-title: 內嵌授權
title: 內嵌授權
uuid: e3d55376-07de-479c-9a53-04bc8071ced4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 內嵌授權{#embedding-licenses}

一旦內容已經加密且已預先產生授權，該授權可嵌入加密內容。

如果您想要內嵌授權，則需要取得`com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`的例項。 如果您知道加密內容的類型，請使用`FLVKeyMetaDataUpdater`或`F4VKeyMetaDataUpdater`的建構函式；否則，請使用`MediaProcessorFactory.getMediaProcessor()`根據檢測到的檔案類型返回實例。 然後，您需要建構`KeyMetaDataCallback`並叫用`modifyKeyMetaData()`。 然後，當DRM中繼資料位於加密內容時，就會叫用您的回呼實作。 您可以根據找到的中繼資料，選擇要內嵌的授權並使用`EmbedLicenseKeyMetaData.setEmbeddedLicenses()`來設定授權。

請參閱參考實作命令列工具[!DNL Samples]目錄中的`com.adobe.flashaccess.samples.licenseembedder.EmbedLicense`，以取得示範內嵌授權的范常式式碼。

>[!NOTE]
>
>Adobe Primetime DRM 2.0用戶端會忽略內嵌在內容中的任何授權，然後嘗試從中繼資料中指定的授權伺服器取得授權。 不過，如果中繼資料指出沒有可用的授權伺服器，則Primetime DRM 2.0用戶端必須先升級，您才能檢視內容。

