---
title: 儲存憑證
description: 儲存憑證
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# 儲存憑據{#storing-credentials}

Primetime DRM SDK支援儲存憑證的不同方式，包括使用硬體安全模組(HSM)或以PKCS12檔案。 當需要私密金鑰時，SDK會使用憑證（公開金鑰憑證和相關的私密金鑰）。 例如，封包者使用憑證來簽署中繼資料；授權伺服器會使用憑證來解密使用授權伺服器或傳輸公開金鑰加密的資料。

您必須密切保護私密金鑰，以確保內容和授權伺服器的安全性。 PKCS12是一種標準的存檔檔案格式，用於儲存使用口令加密的憑據。 （您也可以加密PKCS12檔案並加以簽署。） 副檔名[!DNL .pfx]常用於支援此格式的檔案。

>[!NOTE]
>
>Adobe建議您使用HSM以獲得最高的安全性。
>
>請參閱&#x200B;*Adobe PrimetimeDRM安全部署指南*。

>[!NOTE]
>
>從Java 1.7開始，64位元Sun Java for Windows不再支援Primetime DRM與HSM裝置通訊所需的PKCS11介面。 如果您打算使用HSM，則需要使用32位版本的Java，或使用支援完整PKCS11介面的JDK。

您可以在HSM上保留私密金鑰，並使用Primetime DRM SDK傳入您從HSM取得的憑證。 如果想使用儲存在HSM上的憑據，則需要使用JCE提供程式，該提供程式可與HSM通信，以獲得私鑰的句柄。 然後，您需要將包含公鑰的私鑰句柄、提供程式名稱和證書傳遞到`ServerCredentialFactory.getServerCredential()`。

SunPKCS11提供程式是JCE提供程式的一個示例，可用於訪問HSM上的私鑰。 部分HSM也隨附於JCE提供者隨附的Java SDK。

有關如何使用此提供程式的說明，請參見Sun Java文檔。

PEM和DER是對公鑰證書進行編碼的方法。 PEM是基本64編碼，DER是二進位編碼。 憑證檔案通常使用副檔名[!DNL .cer]、[!DNL .pem]或[!DNL .der]。 只需要公開金鑰時，才會使用憑證。 如果元件只需要公共密鑰才能運行，則建議您為該元件提供證書，而不是憑據或PKCS12檔案。
