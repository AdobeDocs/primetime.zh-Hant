---
title: 加密內容
description: 加密內容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# 加密內容{#encrypting-content}

使用`MediaEncrypter`物件加密視訊內容。 您可以加密僅包含音軌的媒體檔案。 您也可以只套用部分加密；例如，在加密H.264內容時，為低端裝置提供效能。

要使用Java API加密媒體檔案，請執行以下操作：

1. 設定您的開發環境並包括&#x200B;*在項目中設定開發環境*&#x200B;中提及的所有JAR檔案。
1. 建立`ServerCredential`例項以載入簽署所需的憑證。
1. 建立`MediaEncrypter`實例。 如果您不知道您擁有何種類型的檔案，請使用`MediaEncryperFactory`。

1. 使用`DRMParameters`物件指定加密選項。
1. 使用`SignatureParameters`物件設定簽名選項，並將`ServerCredential`例項傳遞至其`setServerCredentials`方法。

1. 使用`V2KeyParameters`物件設定金鑰和授權資訊。 使用`setPolicies`方法設定DRM策略。 通過調用`setLicenseServerUrl`和`setLicenseServerTransportCertificate`方法，設定客戶端聯繫許可證伺服器所需的資訊。 使用`setKeyProtectionOptions`方法設定CEK加密選項，並使用`setCustomProperties`方法設定其自定義屬性。 最後，根據所使用的加密類型，將`DRMKeyParameters`對象轉換為適當的類型(`VideoDRMParameters`、`AudioDRMParameters`)，並設定加密選項。

1. 將輸入和輸出檔案及加密選項傳遞至`MediaEncrypter.encryptContent`方法，以加密內容。

有關如何加密內容的示例代碼，請參見Reference Implementation Command Line Tools [!DNL samples/]目錄中的`com.adobe.flashaccess.samples.mediapackager.EncryptContent`。
