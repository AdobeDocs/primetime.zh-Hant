---
title: 加密內容
description: 加密內容
copied-description: true
exl-id: 84a490ae-af0c-43c5-a849-ed832e83a28d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# 加密內容{#encrypting-content}

加密FLV和F4V內容涉及使用 `MediaEncrypter` 的雙曲餘切值。 您還可以打包僅包含音頻軌道的FLV和F4V檔案。 在為低端設備加密H.264內容時，僅應用部分加密可以提高效能是切實可行的。 在這種情況下，F4V檔案可使用 `F4VDRMParameters.setVideoEncryptionLevel`的雙曲餘切值。

要使用Java API加密FLV或F4V檔案，請執行以下步驟：

1. 設定開發環境並包括「設定項目內的開發環境」中提到的所有JAR檔案。
1. 建立 `ServerCredential` 實例，以載入簽名所需的憑據。
1. 建立 `MediaEncrypter` 實例。 使用 `MediaEncryperFactory` 如果你不知道你擁有的檔案類型。 否則，可以建立 `FLVEncrypter` 或 `F4VEncrypter` 直接輸入。
1. 使用 `DRMParameters` 的雙曲餘切值。
1. 使用 `SignatureParameters` 並傳遞 `ServerCredential` 實例 `setServerCredentials` 的雙曲餘切值。
1. 使用 `V2KeyParameters` 的雙曲餘切值。 使用 `setPolicies` 的雙曲餘切值。 通過調用 `setLicenseServerUrl` 和 `setLicenseServerTransportCertificate` 的雙曲餘切值。 使用 `setKeyProtectionOptions` 方法及其自定義屬性 `setCustomProperties` 的雙曲餘切值。 最後，根據使用的加密類型，將 `DRMKeyParameters` 對象之一 `VideoDRMParameters`。 `AudioDRMParameters`。 `FLVDRMParameters`或 `F4VDRMParameters`，並設定加密選項。
1. 通過將輸入和輸出檔案和加密選項傳遞到 `MediaEncrypter.encryptContent` 的雙曲餘切值。

有關演示如何加密內容的示例代碼，請參見 `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 在「參考實現」命令行工具「示例」目錄中。
