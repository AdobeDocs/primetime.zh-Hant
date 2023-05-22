---
title: 儲存憑據
description: 儲存憑據
copied-description: true
exl-id: ceb1bc19-56a0-47ce-affd-ce4ecb896c3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 儲存憑據{#storing-credentials}

Mighide DRM SDK支援儲存憑據的不同方法，包括使用硬體安全模組(HSM)或作為PKCS12檔案。 當需要私鑰時，SDK使用憑據（公鑰證書和關聯的私鑰）。 例如，打包員使用憑據來簽署元資料；許可證伺服器使用憑據解密已使用許可證伺服器或傳輸公鑰加密的資料。

必須密切保護私鑰，以確保內容和許可證伺服器的安全。 PKCS12是標準存檔檔案格式，用於儲存使用密碼加密的憑據。 （您還可以對PKCS12檔案本身進行加密和簽名。） 檔案副檔名 [!DNL .pfx] 通常用於支援此格式的檔案。

>[!NOTE]
>
>Adobe建議您使用HSM來實現最高安全性。
>
>查看 *Adobe PrimetimeDRM安全部署指南* 的子菜單。

>[!NOTE]
>
>從Java 1.7開始，64位Sun Java for Windows不再支援Mogina時DRM與HSM設備通信所需的PKCS11介面。 如果計畫使用HSM，則需要使用32位版本的Java，或使用支援完整PKCS11介面的JDK。

您可以在HSM上保留私鑰，並使用黃金時段DRM SDK在從HSM獲取的憑據中傳遞。 如果要使用儲存在HSM上的憑據，則需要使用可與HSM通信的JCE提供程式來獲取私鑰的句柄。 然後，您需要將包含公鑰的私鑰句柄、提供程式名稱和證書傳遞給 `ServerCredentialFactory.getServerCredential()`。

SunPKCS11提供程式表示JCE提供程式的一個示例，您可以使用該提供程式訪問HSM上的私鑰。 某些HSM還隨JCE提供程式捆綁的Java SDK提供。

有關如何使用此提供程式的說明，請參見Sun Java文檔。

PEM和DER是對公鑰證書進行編碼的方法。 PEM是base-64編碼，DER是二進位編碼。 證書檔案通常使用副檔名 [!DNL .cer]。 [!DNL .pem]或 [!DNL .der]。 只需要公鑰時使用證書。 如果元件只需要公鑰才能運行，建議您向該元件提供證書，而不是提供憑據或PKCS12檔案。
