---
description: 如果您使用Adobe Primetime DRM Professional，則可以在內容中預先產生授權和內嵌授權。 此功能可與增強型授權鏈結結合，以便Leaf授權預先產生並內嵌於內容中，使用者端可以從授權伺服器要求Root授權（繫結至電腦或網域）。 或者，使用者端應用程式可以實作一個工作流程，讓裝置預先向伺服器註冊，伺服器預先產生繫結到該裝置的授權，使用者端從簡單的HTTP Web伺服器擷取其授權。
title: 預先產生授權
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 預先產生授權 {#pre-generating-licenses}

如果您使用Adobe Primetime DRM Professional，則可以在內容中預先產生授權和內嵌授權。 此功能可與增強型授權鏈結結合，以便Leaf授權預先產生並內嵌於內容中，使用者端可以從授權伺服器要求Root授權（繫結至電腦或網域）。 或者，使用者端應用程式可以實作一個工作流程，讓裝置預先向伺服器註冊，伺服器預先產生繫結到該裝置的授權，使用者端從簡單的HTTP Web伺服器擷取其授權。

如果您想要預先產生授權，您必須使用 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 若要取得 `LicenseFactory`. 您必須指定License Server認證，才能簽署此工廠產生的授權。 此類別支援不使用授權鏈結產生Leaf授權，以及使用產生Leaf和Root授權 [增強授權鏈結](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

產生Leaf授權時，您必須指定套用的內容中繼資料 `initContentInfo()`. 如果中繼資料包含多個DRM原則，或者如果您要使用尚未包含在中繼資料中的DRM原則，您必須使用 `setSelectedPolicy()` 指定DRM政策以產生許可證。 如果您使用「DRM原則更新清單」來追蹤DRM原則的更新，則可以在初始化中繼資料之前，將「DRM原則更新清單」提供給「許可證工廠」 `setPolicyUpdateList()`.

產生Root授權時，必須指定內容中繼資料，如上所述。 或者，您可以套用DRM原則來產生Root許可證( `setSelectedPolicy()`)和授權伺服器URL ( `setLicenseServerURL()`)而非中繼資料。

>[!NOTE]
>
>即使沒有Adobe Primetime DRM License Server可供使用者端要求授權，也需要License Server URL。 在此情況下，授權伺服器URL應指定識別授權簽發者的URL。

如果DRM原則使用增強型授權鏈結，您必須指定授權伺服器認證以解密DRM原則中的根加密金鑰( `setRootKeyRetrievalInfo()`)。

如果DRM原則需要領域繫結授權，您必須使用 `setDomainCAs()` 指定授權伺服器接受網域權杖的網域發行者。 必須提供一個或多個網域CA憑證才能驗證授權收件者。

如果DRM政策要求iOS裝置遠端金鑰傳遞，您必須套用金鑰伺服器憑證 `setKeyServerCertificate()` 除非正在產生鏈結的Leaf。

如果您要產生授權，則必須叫用 `generateLicense()` 並指定授權型別（分葉或根）以及一或多個收件者憑證。 根據DRM原則中指定的要求，收件者憑證代表機器憑證或網域憑證。 如果您產生鏈結分葉，則不需要收件者。 產生授權後，您可以覆寫DRM政策中指定的使用規則。 最後，您需要叫用 `signLicense()` 簽署授權並取得 `PreGeneratedLicense`. 現在可以儲存授權(使用 `getBytes()` 以擷取序列化授權或內嵌於加密內容中。

另請參閱 [內嵌授權](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

另請參閱 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 在參考實作命令列工具「範例」目錄中，取得如何示範預先產生授權的範常式式碼。
