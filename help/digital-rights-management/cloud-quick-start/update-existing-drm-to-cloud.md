---
title: 更新現有DRM內容以使用雲端DRM （可選）
description: 更新現有DRM內容以使用雲端DRM （可選）
copied-description: true
exl-id: 89b1e99a-cb28-4524-9c47-f71f92d3753d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# 更新現有DRM內容以使用雲端DRM （可選） {#update-existing-drm-content-to-use-cloud-drm-optional}

如果您有受Primetime DRM保護的現有內容庫，可以「重新標頭」現有內容以使用Primetime Cloud DRM服務，而不必重新封裝/加密原始來源檔案。 重新標頭化內容只會更新HLS資訊清單中內容的DRM中繼資料。 它不會執行原始資產的任何解密/重新加密。 如果無法使用原始來源內容，或是擔心重新封裝大型程式庫所需的資源量，此選項可能會很實用。

您可以使用Primetime DRM Java SDK以程式設計方式更新中繼資料。 此外， [!DNL OfflinePackager.jar] 本保護套件隨附的命令列工具也可以使用 `-drm_refresh` 選項。

## 重新標頭詳細資料 {#section_3F3980D8E775450588C64E02A8448189}

重新調整標題必須更新以下欄位才能使用CloudDRM：

* 授權伺服器URL (至 [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* 授權伺服器憑證（至CloudDRM授權伺服器憑證）
* 傳輸憑證（到CloudDRM傳輸憑證）
* 封裝者認證（至您已啟動以與CloudDRM一起使用的封裝者認證）

## 尋找DRM中繼資料 {#section_28721CB7966F40708AEC8637F2E9BB72}

使用HTTP技術（例如HDS或HLS）的內容會利用參考Adobe存取DRM中繼資料的資訊清單。 在HDS中，中繼資料會由 `<drmmeta>` 標籤之間，而在HLS中，它由 `#EXT-X-FAXS-CM` 標籤之間。 在任一案例中，中繼資料都可內嵌在資訊清單中當作base-64編碼的blob，或作為二進位檔案從外部參照。 如果資訊清單中內嵌/內嵌中繼資料，您可能需要先將中繼資料以base64解碼為二進位資料，才能使用該資料將DRM中繼資料具現化。

## 使用隨附的OfflinePackger.jar {#section_37C2091856E44AA380D742C72B4DD1A7}

提供 `-drm_refresh option` 至命令列。 將使用更新的DRM中繼資料建立新的資訊清單檔案，但不會重新加密內容。

## 使用Primetime DRM Java SDK重新調整標題 {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

更新現有的DRM中繼資料可以透過使用程式化方法的Primetime DRM (前身為Adobe存取DRM) Java SDK來完成。 如需詳細資訊，請參閱 [!DNL RegenerateMetadata.java] 中的程式碼範例 [!DNL /Reference Implmentation/Command Line Tools/samples/] SDK的套件。 Adobe存取Java SDK不屬於此CloudDRM保護套件，必須直接從Adobe取得。 如需進一步詳細資訊，請聯絡您的Adobe業務連絡人。
