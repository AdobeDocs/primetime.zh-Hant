---
description: 如果您使用Adobe Primetime DRM Professional，則可預先產生授權並將授權內嵌在內容中。 此功能可與「增強授權鏈結」結合，使得Leaf授權已預先產生並內嵌在內容中，而用戶端可向授權伺服器要求根授權（系結至機器或網域）。 或者，客戶端應用程式可以實施一個工作流，其中設備向伺服器預註冊，伺服器預生成綁定到該設備的許可證，並且客戶端從簡單的HTTP Web伺服器檢索其許可證。
seo-description: 如果您使用Adobe Primetime DRM Professional，則可預先產生授權並將授權內嵌在內容中。 此功能可與「增強授權鏈結」結合，使得Leaf授權已預先產生並內嵌在內容中，而用戶端可向授權伺服器要求根授權（系結至機器或網域）。 或者，客戶端應用程式可以實施一個工作流，其中設備向伺服器預註冊，伺服器預生成綁定到該設備的許可證，並且客戶端從簡單的HTTP Web伺服器檢索其許可證。
seo-title: 預先產生的授權
title: 預先產生的授權
uuid: aa7d5038-5a9b-40a2-a240-266622158b43
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---


# 預先產生授權{#pre-generating-licenses}

如果您使用Adobe Primetime DRM Professional，則可預先產生授權並將授權內嵌在內容中。 此功能可與「增強授權鏈結」結合，使得Leaf授權已預先產生並內嵌在內容中，而用戶端可向授權伺服器要求根授權（系結至機器或網域）。 或者，客戶端應用程式可以實施一個工作流，其中設備向伺服器預註冊，伺服器預生成綁定到該設備的許可證，並且客戶端從簡單的HTTP Web伺服器檢索其許可證。

如果您想要預先產生授權，必須使用`com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()`才能取得`LicenseFactory`的例項。 您必須指定授權伺服器憑證才能簽署此工廠產生的授權。 此類別支援產生Leaf授權而無授權鏈結，並支援使用[增強授權鏈結](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md)產生Leaf和Root授權。

當您產生葉片授權時，必須指定套用`initContentInfo()`的內容中繼資料。 如果元資料包含多個DRM策略，或者如果您想要使用未包含在元資料中的DRM策略，則必須使用`setSelectedPolicy()`指定DRM策略以生成許可。 如果您使用DRM策略更新清單來跟蹤DRM策略的更新，則可以在使用`setPolicyUpdateList()`初始化元資料之前，將DRM策略更新清單提供給許可證工廠。

當您產生根授權時，您必須如上所述指定內容中繼資料。 或者，您也可以套用DRM原則(`setSelectedPolicy()`)和授權伺服器URL(`setLicenseServerURL()`)來產生根授權，而非中繼資料。

>[!NOTE]
>
>即使沒有Adobe Primetime DRM License Server，用戶端也必須取得授權伺服器URL。 在這種情況下，「授權伺服器URL」應指定識別授權發行者的URL。

如果DRM策略使用「增強的許可連結」，則必須指定「許可證伺服器」憑據以解密DRM策略(`setRootKeyRetrievalInfo()`)中的根加密密鑰。

如果DRM策略需要域綁定許可證，則必須使用`setDomainCAs()`指定許可證伺服器接受域Token的域發行器。 必須提供一或多個網域CA憑證才能驗證授權收件者。

如果DRM策略要求對iOS設備進行遠程密鑰傳遞，則必須通過應用`setKeyServerCertificate()`來提供密鑰伺服器證書，除非生成鏈式葉。

如果要生成許可證，必須調用`generateLicense()`並指定許可證類型（葉或根）和一個或多個接收者證書。 收件者憑證代表機器憑證或網域憑證，視DRM原則中指定的要求而定。 如果您產生連結葉，則不需要收件者。 在產生授權後，您可以覆寫已在DRM政策中指定的使用規則。 最後，您需要叫用`signLicense()`來簽署授權並取得`PreGeneratedLicense`的例項。 現在可以儲存授權（使用`getBytes()`擷取序號的授權或內嵌在加密的內容中）。

請參閱[內嵌授權](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md)。

請參閱參考實作命令列工具&quot;samples&quot;目錄中的`com.adobe.flashaccess.samples.licensegen.GenerateLicense`，以取得示範預先產生之授權的范常式式碼。
