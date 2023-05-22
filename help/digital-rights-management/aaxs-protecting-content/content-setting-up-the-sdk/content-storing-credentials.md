---
title: 儲存憑據
description: 儲存憑據
copied-description: true
exl-id: 42bccf3a-307f-4763-8b02-f983bcc2e131
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 儲存憑據{#storing-credentials}

SDK支援多種儲存憑據的方法（公鑰證書及其關聯的私鑰），包括在HSM上或作為PKCS12檔案。 在需要私鑰時使用憑據（例如，打包程式對元資料進行簽名，或許可證伺服器對使用許可證伺服器或傳輸公鑰加密的資料進行解密）。 必須嚴密保護私鑰，以確保內容和許可證伺服器的安全。 PKCS12是包含使用密碼加密的憑據的檔案的標準格式。 檔案副檔名.pfx通常用於此格式的檔案。

>[!NOTE]
>
>Adobe建議使用HSM來實現最高安全性。 有關詳細資訊，請參閱Adobe訪問安全部署指南。

>[!NOTE]
>
>從Java1.7開始，64位Sun Java for Windows不支援AdobeAccess DRM與HSM設備通信所需的PKCS11介面。 如果您計畫使用HSM，請使用32位版本的Java，或使用支援完整PKCS11介面的JDK。

您可以在硬體安全模組(HSM)上保留私鑰，並使用SDK在從HSM獲取的憑據中傳遞。 要使用儲存在HSM上的憑據，請使用可與HSM通信的JCE提供程式獲取私鑰的句柄。 然後，將包含公鑰的私鑰句柄、提供程式名稱和證書傳遞到 `ServerCredentialFactory.getServerCredential()`。

SunPKCS11提供程式是JCE提供程式的一個示例，該提供程式可用於訪問HSM上的私鑰（有關使用此提供程式的說明，請參見Sun Java文檔）。 某些HSM還附帶Java SDK，該SDK包括JCE提供程式。

PEM和DER是對公鑰證書進行編碼的兩種方式。 PEM是base-64編碼，DER是二進位編碼。 證書檔案通常使用副檔名.cer、.pem。 或.der。 證書僅在需要公鑰的位置使用。 如果元件只需要公鑰才能運行，則最好向該元件提供證書，而不是憑據或PKCS12檔案。
