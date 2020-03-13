---
seo-title: 加密內容
title: 加密內容
uuid: ea71154e-557b-447e-bc14-208232f00be1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 加密內容{#encrypting-content}

加密FLV和F4V內容需使用物 `MediaEncrypter` 件。 您也可以封裝僅包含音軌的FLV和F4V檔案。 當加密適用於低端裝置的H.264內容時，只套用部分加密可能很實用，以提升效能。 在這種情況下，可使用該方法對F4V檔案進行部分 `F4VDRMParameters.setVideoEncryptionLevel`加密。

若要使用Java API加密FLV或F4V檔案，請執行下列步驟：

1. 設定您的開發環境，並包括在項目中設定開發環境中提到的所有JAR檔案。
1. 建立 `ServerCredential` 例項以載入簽署所需的認證。
1. 建立例 `MediaEncrypter` 項。 如果您 `MediaEncryperFactory` 不知道您擁有的檔案類型，請使用。 否則，您可以直接 `FLVEncrypter` 建立 `F4VEncrypter` 或。
1. 使用物件指定加密 `DRMParameters` 選項。
1. 使用物件設定簽名選 `SignatureParameters` 項，並將執 `ServerCredential` 行個體傳遞至 `setServerCredentials` 方法。
1. 使用物件設定金鑰和授權 `V2KeyParameters` 資訊。 使用方法設定策 `setPolicies` 略。 設定用戶端透過呼叫和方法來連絡授權伺服器所需 `setLicenseServerUrl` 的 `setLicenseServerTransportCertificate` 資訊。 使用方法設定CEK加密選 `setKeyProtectionOptions` 項，並使用方法設定其自定義 `setCustomProperties` 屬性。 最後，根據所使用的加密類型，將對 `DRMKeyParameters` 像轉換為 `VideoDRMParameters`、 `AudioDRMParameters`、 `FLVDRMParameters`或，並 `F4VDRMParameters`設定加密選項。
1. 將輸入和輸出檔案以及加密選項傳遞至方法，以加密 `MediaEncrypter.encryptContent` 內容。

如需示範如何加密內容的范常式式碼，請 `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 參閱參考實作命令列工具「範例」目錄。
