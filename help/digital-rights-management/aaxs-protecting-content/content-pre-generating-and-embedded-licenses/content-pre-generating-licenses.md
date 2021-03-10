---
title: 預先產生的授權
description: 預先產生的授權
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 預先產生授權{#pre-generating-licenses}

若要預先產生授權，請使用`com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()`取得`LicenseFactory`的例項。 必須指定「授權伺服器」憑證，才能簽署此工廠產生的授權。 此類別支援產生Leaf授權而無授權鏈結，並支援使用[增強授權鏈結](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md)產生Leaf和Root授權。

產生葉片授權時，必須使用`initContentInfo()`指定內容中繼資料。 如果中繼資料包含多個原則，或您想要使用未在中繼資料中的原則，請使用`setSelectedPolicy()`指定用來產生授權的原則。 如果使用策略更新清單來跟蹤策略的更新，則可以在使用`setPolicyUpdateList()`初始化元資料之前，將策略更新清單提供到許可證工廠。

當產生根授權時，內容中繼資料可如上所述指定。 或者，您可以使用原則(`setSelectedPolicy()`)和授權伺服器URL(`setLicenseServerURL()`)來產生根授權，而非中繼資料。

>[!NOTE]
>
>即使沒有Adobe存取授權伺服器供用戶端要求授權，仍需要授權伺服器URL。 在這種情況下，「授權伺服器URL」應指定識別授權發行者的URL。

如果策略使用「增強的許可證連結」，則必須指定許可證伺服器憑據才能解密策略(`setRootKeyRetrievalInfo()`)中的根加密密鑰。

如果策略需要域綁定許可證，請使用`setDomainCAs()`指定許可證伺服器將接受域Token的域發行器。 必須提供一或多個網域CA憑證才能驗證授權收件者。

如果策略要求對iOS設備進行遠程密鑰傳遞，則必須使用`setKeyServerCertificate()`提供密鑰伺服器證書，除非生成鏈式葉。

若要產生授權，請叫用`generateLicense()`並指定授權類型（Leaf或Root）和一或多個收件者憑證。 收件者憑證可以是機器憑證或網域憑證，視原則中指定的要求而定。 如果您要產生連結葉，則不需要收件者。 在產生授權後，可以覆寫原則中指定的使用規則。 最後，請叫用`signLicense()`來簽署授權並取得`PreGeneratedLicense`的例項。 授權現在可儲存至檔案（使用`getBytes()`擷取序號的授權）或內嵌在加密的內容中。 請參閱[內嵌授權](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md)。

有關演示預生成許可證的示例代碼，請參閱參考實施命令行工具&quot;samples&quot;目錄中的`com.adobe.flashaccess.samples.licensegen.GenerateLicense`。
