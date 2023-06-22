---
title: 儲存認證
description: 儲存認證
copied-description: true
exl-id: 42bccf3a-307f-4763-8b02-f983bcc2e131
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 儲存認證{#storing-credentials}

SDK支援多種憑證儲存方式（公開金鑰憑證及其關聯的私密金鑰），包括在HSM上或當作PKCS12檔案。 當需要私密金鑰時（例如，封裝者需要簽署中繼資料，或授權伺服器需要解密使用授權伺服器或傳輸公開金鑰加密的資料），就會使用認證。 必須嚴密保護私密金鑰，以確保您的內容和License Server的安全性。 PKCS12是檔案的標準格式，其中包含使用密碼加密的認證。 檔案副檔名.pfx通常用於此格式的檔案。

>[!NOTE]
>
>Adobe建議使用HSM以獲得最大安全性。 如需詳細資訊，請參閱Adobe存取安全部署准則。

>[!NOTE]
>
>自Java1.7起，Windows適用的64位元Sun Java不支援Adobe存取DRM與HSM裝置通訊所需的PKCS11介面。 如果您打算使用HSM，請使用32位元版本的Java，或使用支援完整PKCS11介面的JDK。

您可以在Hardware Security Module (HSM)上保留私密金鑰，並使用SDK傳遞您從HSM取得的認證。 若要使用儲存在HSM上的認證，請使用可與HSM通訊的JCE提供者來取得私密金鑰的控制碼。 然後，將私密金鑰控制代碼、提供者名稱和包含公開金鑰的憑證傳遞至 `ServerCredentialFactory.getServerCredential()`.

SunPKCS11提供者是JCE提供者的一個範例，可用來存取HSM上的私密金鑰（請參閱Sun Java檔案以瞭解使用此提供者的指示）。 部分HSM也隨附Java SDK，內含JCE提供者。

PEM和DER是兩種編碼公開金鑰憑證的方式。 PEM是base-64編碼，而DER是二進位編碼。 憑證檔案通常使用副檔名.cer、.pem。 或.der. 憑證用於只需要公開金鑰的地方。 如果元件僅需要公開金鑰才能運作，最好向該元件提供憑證，而不是認證或PKCS12檔案。
