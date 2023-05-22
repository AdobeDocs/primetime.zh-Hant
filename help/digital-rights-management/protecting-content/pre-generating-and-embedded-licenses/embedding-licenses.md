---
title: 嵌入許可證
description: 嵌入許可證
copied-description: true
exl-id: 8cd58808-73fb-4635-9a75-0520430f6b3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 嵌入許可證 {#embedding-licenses}

一旦內容被加密並且許可證被預生成，許可證可以被嵌入到加密內容中。

如果要嵌入許可證，則需要獲取 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`。 如果您知道加密內容的類型，請使用 `FLVKeyMetaDataUpdater` 或 `F4VKeyMetaDataUpdater`;否則，使用 `MediaProcessorFactory.getMediaProcessor()` 返回基於檢測到的檔案類型的實例。 然後你需要構造 `KeyMetaDataCallback` 調用 `modifyKeyMetaData()`。 然後，當DRM元資料位於加密內容中時，將調用回調實現。 根據找到的元資料，您可以選擇要嵌入的許可證並使用 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`。

請參閱 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 在「參考實現」命令行工具中 [!DNL Samples] 示例代碼的目錄。

>[!NOTE]
>
>Adobe PrimetimeDRM 2.0客戶端忽略嵌入在內容中的任何許可證，然後嘗試從在元資料中指定的許可證伺服器獲取許可證。 但是，如果元資料指示沒有可用的許可證伺服器，則需要先升級Mighine DRM 2.0客戶端，然後才能查看內容。
