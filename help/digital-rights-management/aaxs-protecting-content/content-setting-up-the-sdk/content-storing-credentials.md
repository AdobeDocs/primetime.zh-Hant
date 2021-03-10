---
title: 儲存憑證
description: 儲存憑證
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# 儲存憑據{#storing-credentials}

SDK支援多種儲存憑證的方式（公開金鑰憑證及其相關的私密金鑰），包括在HSM或PKCS12檔案中。 憑證會在需要私密金鑰時使用（例如，封包員簽署中繼資料，或授權伺服器解密使用授權伺服器或傳輸公用金鑰加密的資料）。 私密金鑰必須嚴加保護，以確保內容和授權伺服器的安全性。 PKCS12是包含使用口令加密的憑據的檔案的標準格式。 副檔名。pfx常用於此格式的檔案。

>[!NOTE]
>
>Adobe建議使用HSM以發揮最大的安全性。 如需詳細資訊，請參閱Adobe存取安全部署准則。

>[!NOTE]
>
>從Java1.7開始，64位Sun Java for Windows不支援AdobeAccess DRM與HSM設備通信所需的PKCS11介面。 如果您打算使用HSM，請使用32位版本的Java，或使用支援完整PKCS11介面的JDK。

您可以在硬體安全性模組(HSM)上保留私密金鑰，並使用SDK從HSM取得的憑證。 要使用儲存在HSM上的憑據，請使用可與HSM通信的JCE提供程式來獲取私鑰的句柄。 然後，將包含公鑰的私鑰句柄、提供者名稱和證書傳遞到`ServerCredentialFactory.getServerCredential()`。

SunPKCS11提供程式是JCE提供程式的一個示例，該提供程式可用於訪問HSM上的私鑰（有關使用此提供程式的說明，請參見Sun Java文檔）。 有些HSM也隨附Java SDK，其中包含JCE提供者。

PEM和DER是兩種對公鑰證書進行編碼的方法。 PEM是基本64編碼，DER是二進位編碼。 憑證檔案通常使用副檔名。cer、.pem。 或。der。 憑證僅用於需要公開金鑰的地方。 如果元件只需要公共密鑰才能運行，則最好為該元件提供證書，而不是憑據或PKCS12檔案。
