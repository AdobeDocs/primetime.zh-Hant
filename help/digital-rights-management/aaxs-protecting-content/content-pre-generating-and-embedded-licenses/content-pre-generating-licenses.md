---
title: 預先產生授權
description: 預先產生授權
copied-description: true
exl-id: 2be8674c-736f-4ed3-b952-f661bf3ff48f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 預先產生授權{#pre-generating-licenses}

若要預先產生授權，請使用 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 若要取得「 」的例項 `LicenseFactory`. 必須指定License Server認證，才能簽署此工廠產生的授權。 此類別支援不使用授權鏈結來產生Leaf授權，以及使用 [增強授權鏈結](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

產生Leaf授權時，必須使用指定內容中繼資料 `initContentInfo()`. 如果中繼資料包含多個原則，或您想使用中繼資料中沒有的原則，請使用 `setSelectedPolicy()` 指定用來產生授權的原則。 如果您使用原則更新清單來追蹤原則的更新，則可以使用在初始化中繼資料之前提供原則更新清單給授權工廠 `setPolicyUpdateList()`.

產生Root授權時，可依照上述方式指定內容中繼資料。 或者，可以使用原則( `setSelectedPolicy()`)和授權伺服器URL ( `setLicenseServerURL()`)而非中繼資料。

>[!NOTE]
>
>即使沒有使用者端可要求授權的Adobe存取授權伺服器，也需要授權伺服器URL。 在此情況下，授權伺服器URL應指定識別授權簽發者的URL。

如果原則使用增強型授權鏈結，則必須指定授權伺服器認證，才能解密原則中的根加密金鑰( `setRootKeyRetrievalInfo()`)。

如果原則需要網域繫結授權，請使用 `setDomainCAs()` 以指定授權伺服器將接受網域權杖的網域發行者。 必須提供一個或多個網域CA憑證，才能驗證授權收件者。

如果原則需要iOS裝置的遠端金鑰傳遞，則必須使用下列專案提供金鑰伺服器憑證： `setKeyServerCertificate()`，除非產生鏈結的葉。

若要產生授權，請叫用 `generateLicense()` 和指定授權型別（分葉或根）和一個或多個收件者憑證。 收件者憑證會是電腦憑證或網域憑證，視原則中指定的要求而定。 如果您產生鏈結分葉，則不需要收件者。 產生授權後，可以覆寫原則中指定的使用規則。 最後，叫用 `signLicense()` 以簽署授權並取得 `PreGeneratedLicense`. 授權現在可以儲存至檔案(使用 `getBytes()` 以擷取序列化授權)或內嵌在加密內容中。 請參閱， [內嵌授權](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

如需示範預先產生之授權的範常式式碼，請參閱 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 在「參考實作命令列工具」的「範例」目錄中。
