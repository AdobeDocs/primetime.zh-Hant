---
title: 內嵌授權
description: 內嵌授權
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 內嵌授權{#embedding-licenses}

一旦內容已經加密且已預先產生授權，該授權可嵌入加密內容。

若要嵌入授權，請取得`com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`的例項。 如果您知道加密內容的類型，請使用`FLVKeyMetaDataUpdater`或`F4VKeyMetaDataUpdater`的建構函式；否則，請使用`MediaProcessorFactory.getMediaProcessor()`根據檢測到的檔案類型返回實例。 構建`KeyMetaDataCallback`並調用`modifyKeyMetaData()`。 當DRM中繼資料位於加密的內容中時，將會呼叫您的回呼實作。 您可以根據找到的中繼資料，選擇要內嵌的授權並使用`EmbedLicenseKeyMetaData.setEmbeddedLicenses()`來設定授權。

如需示範內嵌授權的范常式式碼，請參閱參考實作命令列工具&quot;Samples&quot;目錄中的`com.adobe.flashaccess.samples.licenseembedder.EmbedLicense`。

>[!NOTE]
>
>AdobeAccess 2.0用戶端會忽略內容中內嵌的任何授權，並會嘗試從中繼資料中指定的授權伺服器取得授權。 不過，如果中繼資料指出沒有可用的授權伺服器，AdobeAccess 2.0用戶端將需要升級才能檢視內容。

請參閱[帶外授權](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md)。
