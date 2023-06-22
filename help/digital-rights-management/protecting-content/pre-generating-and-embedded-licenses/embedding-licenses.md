---
title: 內嵌授權
description: 內嵌授權
copied-description: true
exl-id: 8cd58808-73fb-4635-9a75-0520430f6b3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 內嵌授權 {#embedding-licenses}

一旦內容已加密且已預先產生授權，授權可以嵌入到加密內容中。

如果您想要內嵌授權，您需要取得 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. 如果您知道加密內容的型別，請使用建構函式 `FLVKeyMetaDataUpdater` 或 `F4VKeyMetaDataUpdater`；否則，請使用 `MediaProcessorFactory.getMediaProcessor()` 以根據偵測到的檔案型別傳回執行個體。 然後您需要建構 `KeyMetaDataCallback` 並叫用 `modifyKeyMetaData()`. 然後，當DRM中繼資料位於加密內容中時，就會叫用回呼實作。 根據找到的中繼資料，您可以選擇要內嵌的授權並使用設定授權 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

另請參閱 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 在參考實作命令列工具中 [!DNL Samples] 示範內嵌授權之範常式式碼的目錄。

>[!NOTE]
>
>Adobe Primetime DRM 2.0使用者端會忽略內嵌於內容中的任何授權，然後嘗試從中繼資料中指定的授權伺服器取得授權。 不過，如果中繼資料指出沒有可用的授權伺服器，則必須先升級Primetime DRM 2.0使用者端，才能檢視內容。
