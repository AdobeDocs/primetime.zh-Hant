---
title: 更新現有DRM內容以使用雲DRM（可選）
description: 更新現有DRM內容以使用雲DRM（可選）
copied-description: true
exl-id: 89b1e99a-cb28-4524-9c47-f71f92d3753d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# 更新現有DRM內容以使用雲DRM（可選） {#update-existing-drm-content-to-use-cloud-drm-optional}

如果您擁有由Mighile DRM保護的現有內容庫，則可以「重新標頭」現有內容以使用Mighile Cloud DRM服務，而不必重新打包/加密原始源檔案。 重新調整內容只是更新HLS清單中內容的DRM元資料。 它不會對原始資產執行任何非加密/重新加密。 如果原始源內容不可用，或者擔心重新打包大型庫所需的資源量，則此選項可能很有用。

可以使用Mighine DRM Java SDK以寫程式方式更新元資料。 另外， [!DNL OfflinePackager.jar] 此保護套件中附帶的命令行工具也可以使用 `-drm_refresh` 的雙曲餘切值。

## 重新報頭詳細資訊 {#section_3F3980D8E775450588C64E02A8448189}

重新命名必須更新以下欄位才能使用CloudDRM:

* 許可證伺服器URL(至 [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* 許可證伺服器證書（到CloudDRM許可證伺服器證書）
* 傳輸證書（到CloudDRM傳輸證書）
* 打包器憑據（對已激活以與CloudDRM一起使用的打包器憑據）

## 查找DRM元資料 {#section_28721CB7966F40708AEC8637F2E9BB72}

使用HTTP技術（如HDS或HLS）的內容使用引用Adobe訪問DRM元資料的清單。 在HDS中，元資料由 `<drmmeta>` 標籤，在HLS中， `#EXT-X-FAXS-CM` 標籤。 在任一情形中，元資料都可以內聯地包含在清單中，作為base-64編碼的blob，或以二進位檔案在外部引用。 如果元資料嵌入/內聯在清單中，則在使用該資料實例化DRM元資料之前，您可能必須首先將元資料基64解碼成二進位資料。

## 使用包含的OfflinePacakger.jar {#section_37C2091856E44AA380D742C72B4DD1A7}

提供 `-drm_refresh option` 命令行。 將使用更新的DRM元資料建立新的清單檔案，而不會重新加密內容。

## 使用黃金時段DRM Java SDK重新標頭 {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

通過使用用於寫程式方法的Mighine DRM(以前稱為Adobe訪問DRM)Java SDK，可以完成更新現有DRM元資料。 有關詳細資訊，請參閱 [!DNL RegenerateMetadata.java] 代碼示例 [!DNL /Reference Implmentation/Command Line Tools/samples/] 軟體包。 Adobe訪問Java SDK不是此CloudDRM保護套件的一部分，必須直接從Adobe獲取。 請聯繫您的Adobe業務聯繫人，以瞭解更多詳細資訊。
