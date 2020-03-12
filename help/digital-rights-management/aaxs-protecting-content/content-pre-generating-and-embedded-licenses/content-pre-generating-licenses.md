---
seo-title: 預先產生的授權
title: 預先產生的授權
uuid: 31430753-11f1-4ce5-b402-cf4279119a05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 預先產生的授權{#pre-generating-licenses}

若要預先產生授權，請 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 使用來取得實例 `LicenseFactory`。 必須指定「授權伺服器」憑證，才能簽署此工廠產生的授權。 此類別支援產生Leaf授權而不需授權鏈結，以及Leaf和Root授權與 [Enhanced授權鏈結](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md)。

產生葉片授權時，必須使用指定內容中繼資料 `initContentInfo()`。 如果中繼資料包含多個原則，或您想要使用未在中繼資料中的原則，請使 `setSelectedPolicy()` 用指定用來產生授權的原則。 如果使用策略更新清單跟蹤策略的更新，則可以在使用初始化元資料之前將策略更新清單提供到許可證工廠 `setPolicyUpdateList()`。

當產生根授權時，內容中繼資料可如上所述指定。 或者，您可使用原則( `setSelectedPolicy()`)和授權伺服器URL()來產生根授權，而 `setLicenseServerURL()`非中繼資料。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>即使沒有Adobe Access License Server可供用戶端要求授權，仍需要授權伺服器URL。 在這種情況下，「授權伺服器URL」應指定識別授權發行者的URL。

如果策略使用「增強的許可證連結」，則必須指定許可證伺服器憑據才能解密策略( `setRootKeyRetrievalInfo()`)中的根加密密鑰。

如果原則需要網域系結授權，請 `setDomainCAs()` 使用來指定授權伺服器將接受網域Token的網域發行者。 必須提供一或多個網域CA憑證才能驗證授權收件者。

如果策略要求對iOS設備進行遠程密鑰傳遞，則必須使用密鑰伺服器證書提供， `setKeyServerCertificate()`除非生成鏈式葉。

若要產生授權，請叫 `generateLicense()` 用並指定授權類型（Leaf或Root）和一或多個收件者憑證。 收件者憑證可以是機器憑證或網域憑證，視原則中指定的要求而定。 如果您要產生連結葉，則不需要收件者。 在產生授權後，可以覆寫原則中指定的使用規則。 最後，請 `signLicense()` 叫用以簽署授權並取得實例 `PreGeneratedLicense`。 授權現在可儲存至檔案(用來擷取序 `getBytes()` 列化的授權)或內嵌在加密內容中。 請參閱內嵌 [授權](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md)。

如需示範預先產生之授權的范常式式碼，請 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 參閱參考實作命令列工具「範例」目錄。
