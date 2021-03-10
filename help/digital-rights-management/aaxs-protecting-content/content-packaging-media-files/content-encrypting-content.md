---
title: 加密內容
description: 加密內容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# 加密內容{#encrypting-content}

加密FLV和F4V內容需使用`MediaEncrypter`物件。 您也可以封裝僅包含音軌的FLV和F4V檔案。 當加密適用於低端裝置的H.264內容時，只套用部分加密可能很實用，以提升效能。 在這種情況下，F4V檔案可以使用`F4VDRMParameters.setVideoEncryptionLevel`方法進行部分加密。

若要使用Java API加密FLV或F4V檔案，請執行下列步驟：

1. 設定您的開發環境，並包括在項目中設定開發環境中提到的所有JAR檔案。
1. 建立`ServerCredential`例項以載入簽署所需的憑證。
1. 建立`MediaEncrypter`實例。 如果您不知道您擁有何種類型的檔案，請使用`MediaEncryperFactory`。 否則，您可以直接建立`FLVEncrypter`或`F4VEncrypter`。
1. 使用`DRMParameters`物件指定加密選項。
1. 使用`SignatureParameters`物件設定簽名選項，並將`ServerCredential`例項傳遞至其`setServerCredentials`方法。
1. 使用`V2KeyParameters`物件設定金鑰和授權資訊。 使用`setPolicies`方法設定策略。 通過調用`setLicenseServerUrl`和`setLicenseServerTransportCertificate`方法，設定客戶端聯繫許可證伺服器所需的資訊。 使用`setKeyProtectionOptions`方法設定CEK加密選項，並使用`setCustomProperties`方法設定其自定義屬性。 最後，根據所使用的加密類型，將`DRMKeyParameters`對象轉換為`VideoDRMParameters`、`AudioDRMParameters`、`FLVDRMParameters`或`F4VDRMParameters`中的一個，並設定加密選項。
1. 將輸入和輸出檔案及加密選項傳遞至`MediaEncrypter.encryptContent`方法，以加密內容。

如需示範如何加密內容的范常式式碼，請參閱參考實作命令列工具&quot;samples&quot;目錄中的`com.adobe.flashaccess.samples.mediapackager.EncryptContent`。
