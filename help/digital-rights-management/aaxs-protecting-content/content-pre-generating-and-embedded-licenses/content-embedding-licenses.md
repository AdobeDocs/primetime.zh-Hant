---
title: 內嵌授權
description: 內嵌授權
copied-description: true
exl-id: 63b1bf18-b93d-4305-885a-3a9eee783a03
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 內嵌授權 {#embedding-licenses}

一旦內容已加密且已預先產生授權，授權可以嵌入到加密內容中。

若要內嵌授權，請取得 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. 如果您知道加密內容的型別，請使用建構函式 `FLVKeyMetaDataUpdater` 或 `F4VKeyMetaDataUpdater`；否則，請使用 `MediaProcessorFactory.getMediaProcessor()` 以根據偵測到的檔案型別傳回執行個體。 建構 `KeyMetaDataCallback` 並叫用 `modifyKeyMetaData()`. 當DRM中繼資料位於加密內容中時，將會叫用您的回呼實作。 根據找到的中繼資料，您可以選擇要內嵌的授權並使用設定授權 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

如需示範內嵌授權的範常式式碼，請參閱 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 在「參考實作」命令列工具「Samples」目錄中。

>[!NOTE]
>
>Adobe Access 2.0使用者端將忽略內容中內嵌的任何授權，並嘗試從中繼資料中指定的授權伺服器取得授權。 不過，如果中繼資料指出沒有可用的授權伺服器，則Adobe Access 2.0使用者端必須升級才能檢視內容。

另請參閱 [頻外授權](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
