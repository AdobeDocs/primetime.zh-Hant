---
seo-title: 加密內容
title: 加密內容
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 加密內容{#encrypting-content}

您會使用物件來加密視訊 `MediaEncrypter` 內容。 您可以加密僅包含音軌的媒體檔案。 您也可以只套用部分加密；例如，在加密H.264內容時，可改善低階裝置的效能。

要使用Java API加密媒體檔案，請執行以下操作：

1. 設定您的開發環境，並將「設定開發環境」中提 *及的所有JAR檔案包括在項目* 中。
1. 建立 `ServerCredential` 例項以載入簽署所需的認證。
1. 建立例 `MediaEncrypter` 項。 如果您 `MediaEncryperFactory` 不知道您擁有的檔案類型，請使用。

1. 使用物件指定加密 `DRMParameters` 選項。
1. 使用物件設定簽名選 `SignatureParameters` 項，並將執 `ServerCredential` 行個體傳遞至 `setServerCredentials` 方法。

1. 使用物件設定金鑰和授權 `V2KeyParameters` 資訊。 使用方法設定DRM策 `setPolicies` 略。 設定用戶端透過呼叫和方法來連絡授權伺服器所需 `setLicenseServerUrl` 的 `setLicenseServerTransportCertificate` 資訊。 使用方法設定CEK加密選 `setKeyProtectionOptions` 項，並使用方法設定其自定義 `setCustomProperties` 屬性。 最後，根據所使用的加密類型，將對 `DRMKeyParameters` 像轉換為適當的類型( `VideoDRMParameters`、 `AudioDRMParameters`)，並設定加密選項。

1. 將輸入和輸出檔案以及加密選項傳遞至方法，以加密 `MediaEncrypter.encryptContent` 內容。

有關如何加密內容的示例代碼，請參 `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 見Reference Implementation命令行工具目 [!DNL samples/] 錄。
