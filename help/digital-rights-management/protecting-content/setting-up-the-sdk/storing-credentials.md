---
title: 儲存認證
description: 儲存認證
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 儲存認證{#storing-credentials}

Primetime DRM SDK支援不同的憑證儲存方式，包括使用Hardware Security Module (HSM)或當作PKCS12檔案。 需要私密金鑰時，SDK會使用認證（公開金鑰憑證和相關聯的私密金鑰）。 例如，封裝程式會使用認證來簽署中繼資料；授權伺服器會使用認證來解密已使用License Server或Transport公開金鑰加密的資料。

您必須嚴密保護私密金鑰，以確保您的內容和License Server的安全性。 PKCS12是一種標準封存檔案格式，用於儲存已使用密碼加密的認證。 （您也可以對PKCS12檔案本身進行加密及簽署。） 副檔名 [!DNL .pfx] 通常用於支援此格式的檔案。

>[!NOTE]
>
>Adobe建議您使用HSM以達到最高安全性。
>
>請參閱 *Adobe Primetime DRM安全部署指引* 指南。

>[!NOTE]
>
>從Java 1.7開始，Windows適用的64位元Sun Java不再支援Primetime DRM與HSM裝置通訊所需的PKCS11介面。 如果您計畫使用HSM，則需要使用32位元版本的Java，或使用支援完整PKCS11介面的JDK。

您可以在HSM上保留私密金鑰，並使用Primetime DRM SDK傳遞您從HSM取得的認證。 如果您想要使用儲存在HSM上的認證，則需要使用可與HSM通訊的JCE提供者，以取得私密金鑰的控制碼。 然後，您需要將私密金鑰控制代碼、提供者名稱和包含公開金鑰的憑證傳遞給 `ServerCredentialFactory.getServerCredential()`.

SunPKCS11提供者代表一個JCE提供者的範例，您可以使用它來存取HSM上的私密金鑰。 部分HSM也隨附於JCE提供者隨附的Java SDK。

請參閱Sun Java檔案，以取得如何使用此提供者的指示。

PEM和DER是編碼公開金鑰憑證的方式。 PEM是base-64編碼，而DER是二進位編碼。 憑證檔案通常使用副檔名 [!DNL .cer]， [!DNL .pem]，或 [!DNL .der]. 憑證用於只需要公開金鑰的情況。 如果元件僅需要公開金鑰才能運作，建議您為該元件提供憑證，而非認證或PKCS12檔案。
