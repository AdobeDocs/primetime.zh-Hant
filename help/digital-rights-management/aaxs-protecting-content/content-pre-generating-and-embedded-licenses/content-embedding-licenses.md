---
title: 嵌入許可證
description: 嵌入許可證
copied-description: true
exl-id: 63b1bf18-b93d-4305-885a-3a9eee783a03
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 嵌入許可證 {#embedding-licenses}

一旦內容被加密並且許可證被預生成，許可證可以被嵌入到加密內容中。

要嵌入許可證，請獲取 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`。 如果您知道加密內容的類型，請使用 `FLVKeyMetaDataUpdater` 或 `F4VKeyMetaDataUpdater`;否則，使用 `MediaProcessorFactory.getMediaProcessor()` 返回基於檢測到的檔案類型的實例。 構造 `KeyMetaDataCallback` 調用 `modifyKeyMetaData()`。 當DRM元資料位於加密內容中時，將調用回調實現。 根據找到的元資料，您可以選擇要嵌入的許可證並使用 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`。

有關演示嵌入式許可證的示例代碼，請參見 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 在「參考實現」命令行工具「示例」目錄中。

>[!NOTE]
>
>AdobeAccess 2.0客戶端將忽略內容中嵌入的任何許可證，並將嘗試從元資料中指定的許可證伺服器獲取許可證。 但是，如果元資料指示沒有許可證伺服器可用，則AdobeAccess 2.0客戶端需要升級才能查看內容。

請參閱 [帶外許可證](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md)。
