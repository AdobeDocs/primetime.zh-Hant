---
seo-title: 更新現有的DRM內容以使用Cloud DRM（可選）
title: 更新現有的DRM內容以使用Cloud DRM（可選）
uuid: cfabeb06-210f-45af-b8a6-8e0b03a76103
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# 更新現有的DRM內容以使用Cloud DRM（可選）{#update-existing-drm-content-to-use-cloud-drm-optional}

如果您有受Primetime DRM保護的現有內容庫，則可以「重新標題」現有內容，以使用Primetime Cloud DRM服務，而不必重新封裝／加密原始來源檔案。 重新命名內容只是更新HLS資訊清單中內容的DRM中繼資料。 它不會對原始資產執行任何非加密／重新加密。 如果原始來源內容不可用，或擔心重新封裝大型程式庫所需的資源量，這個選項可能很有用。

您可使用Primetime DRM Java SDK以程式設計方式更新中繼資料。 此外，此保護套件附帶的[!DNL OfflinePackager.jar]命令行工具也可以使用`-drm_refresh`選項完成此任務。

## 重新標題詳細資料{#section_3F3980D8E775450588C64E02A8448189}

重新引導必須更新下列欄位，才能使用CloudDRM:

* 授權伺服器URL(至[!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* 授權伺服器憑證（至CloudDRM授權伺服器憑證）
* 傳輸憑證（至CloudDRM傳輸憑證）
* Packager憑證（至您為搭配CloudDRM使用而啟用的Packager憑證）

## 查找DRM元資料{#section_28721CB7966F40708AEC8637F2E9BB72}

使用HTTP技術（例如HDS或HLS）的內容使用參照Adobe Access DRM中繼資料的資訊清單。 在HDS中，元資料由`<drmmeta>`標籤引用，在HLS中，元資料由`#EXT-X-FAXS-CM`標籤引用。 在任一情況下，中繼資料都可內嵌在資訊清單中，成為基本64編碼的點滴，或以二進位檔案從外部參照。 如果中繼資料內嵌／內嵌於資訊清單中，您可能必須先將中繼資料基本64解碼為二進位資料，再使用該資料來實例化DRM中繼資料。

## 使用隨附的OfflinePacakger.jar {#section_37C2091856E44AA380D742C72B4DD1A7}

將`-drm_refresh option`提供給命令行。 使用更新的DRM中繼資料建立新的資訊清單檔案，而內容則不會重新加密。

## 使用Primetime DRM Java SDK重新標題{#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

更新現有的DRM中繼資料可透過使用Primetime DRM（先前稱為Adobe Access DRM）Java SDK進行程式化方式。 如需詳細資訊，請參閱SDK [!DNL /Reference Implmentation/Command Line Tools/samples/]套件中的[!DNL RegenerateMetadata.java]程式碼範例。 Adobe Access Java SDK不屬於本CloudDRM保護套件，必須直接向Adobe取得。 如需詳細資訊，請連絡您的Adobe業務聯絡人。