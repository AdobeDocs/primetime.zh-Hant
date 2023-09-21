---
title: 儲存認證
description: 儲存認證
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 儲存認證{#storing-credentials}

SDK支援多種憑證儲存方式（公開金鑰憑證及其相關私密金鑰），包括在HSM上或當作PKCS12檔案儲存。 當需要私密金鑰時（例如，封裝者需要簽署中繼資料，或授權伺服器需要解密使用授權伺服器或傳輸公開金鑰加密的資料），就會使用認證。 私密金鑰必須嚴密保護，以確保您的內容和License Server的安全性。 PKCS12是檔案的標準格式，其中包含使用密碼加密的認證。 檔案副檔名.pfx通常用於此格式的檔案。

>[!NOTE]
>
>Adobe建議使用HSM以達到最高安全性。 如需詳細資訊，請參閱Adobe存取安全部署准則。

>[!NOTE]
>
>從Java1.7開始，適用於Windows的64位元Sun Java不支援Adobe存取DRM與HSM裝置通訊所需的PKCS11介面。 如果您打算使用HSM，請使用32位元版本的Java，或使用支援完整PKCS11介面的JDK。

您可以在Hardware Security Module (HSM)上保留私密金鑰，並使用SDK傳遞您從HSM取得的認證。 若要使用儲存在HSM上的認證，請使用可與HSM通訊的JCE提供者取得私密金鑰的控制碼。 然後，將私密金鑰控制代碼、提供者名稱和包含公開金鑰的憑證傳遞至 `ServerCredentialFactory.getServerCredential()`.

SunPKCS11提供者是JCE提供者的一個範例，可用來存取HSM上的私密金鑰（請參閱Sun Java檔案以取得使用此提供者的指示）。 部分HSM也隨附Java SDK，其中包含JCE提供者。

PEM和DER是兩種編碼公開金鑰憑證的方式。 PEM是base-64編碼，而DER是二進位編碼。 憑證檔案通常使用副檔名.cer、.pem。 或.der. 憑證適用於只需要公開金鑰的位置。 如果元件僅需要公開金鑰才能運作，最好向該元件提供憑證，而非認證或PKCS12檔案。
