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

您使用 `MediaEncrypter` 的雙曲餘切值。 您可以加密只包含音頻軌道的媒體檔案。 您也只能應用部分加密；例如，在為低端設備加密H.264內容時提高效能。

要使用Java API加密媒體檔案：

1. 設定開發環境並包括中提及的所有JAR檔案 *建立開發環境* 你的項目。
1. 建立 `ServerCredential` 實例，以載入簽名所需的憑據。
1. 建立 `MediaEncrypter` 實例。 使用 `MediaEncryperFactory` 如果你不知道你擁有的檔案類型。

1. 使用 `DRMParameters` 的雙曲餘切值。
1. 使用 `SignatureParameters` 並傳遞 `ServerCredential` 實例 `setServerCredentials` 的雙曲餘切值。

1. 使用 `V2KeyParameters` 的雙曲餘切值。 使用 `setPolicies` 的雙曲餘切值。 通過調用 `setLicenseServerUrl` 和 `setLicenseServerTransportCertificate` 的雙曲餘切值。 使用 `setKeyProtectionOptions` 方法及其自定義屬性 `setCustomProperties` 的雙曲餘切值。 最後，根據使用的加密類型，將 `DRMKeyParameters` 對象到相應類型( `VideoDRMParameters`。 `AudioDRMParameters`)，並設定加密選項。

1. 通過將輸入和輸出檔案和加密選項傳遞到 `MediaEncrypter.encryptContent` 的雙曲餘切值。

有關顯示如何加密內容的示例代碼，請參見 `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 在「參考實現」命令行工具中 [!DNL samples/] 的子菜單。
