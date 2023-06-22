---
title: 加密內容
description: 加密內容
copied-description: true
exl-id: c6b5d8c7-eda4-40c0-a609-0ebfeba90c04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 加密內容{#encrypting-content}

您使用加密視訊內容 `MediaEncrypter` 物件。 您可以加密僅包含音訊曲目的媒體檔案。 您也可以僅套用部分加密；例如，針對低端裝置加密H.264內容時，可提升效能。

若要使用Java API加密媒體檔案：

1. 設定您的開發環境，並包含中提到的所有JAR檔案 *設定開發環境* 在您的專案中。
1. 建立 `ServerCredential` 執行個體以載入簽署所需的認證。
1. 建立 `MediaEncrypter` 執行個體。 使用 `MediaEncryperFactory` 如果您不知道您有哪種檔案型別。

1. 使用指定加密選項 `DRMParameters` 物件。
1. 使用設定簽名選項 `SignatureParameters` 物件並傳遞 `ServerCredential` 執行個體至其 `setServerCredentials` 方法。

1. 使用設定金鑰和授權資訊 `V2KeyParameters` 物件。 使用設定DRM政策 `setPolicies` 方法。 透過呼叫 `setLicenseServerUrl` 和 `setLicenseServerTransportCertificate` 方法。 使用設定CEK加密選項 `setKeyProtectionOptions` 方法，及其自訂屬性 `setCustomProperties` 方法。 最後，視所使用的加密型別而定，將 `DRMKeyParameters` 物件至適當的型別( `VideoDRMParameters`， `AudioDRMParameters`)，並設定加密選項。

1. 將輸入和輸出檔案及加密選項傳遞至 `MediaEncrypter.encryptContent` 方法。

如需顯示如何加密內容的範常式式碼，請參閱 `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 在參考實作命令列工具中 [!DNL samples/] 目錄。
