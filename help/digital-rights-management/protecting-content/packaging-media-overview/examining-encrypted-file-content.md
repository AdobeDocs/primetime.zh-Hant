---
seo-title: 檢查加密的檔案內容
title: 檢查加密的檔案內容
uuid: 1b3318f6-0850-43f2-9127-c72ea81a1bdf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 檢查加密的檔案內容{#examining-encrypted-file-content}

您可以使用Java API檢查加密媒體檔案的內容。

要檢查加密的檔案內容：

1. 設定您的開發環境並包括所有JAR檔案。 請參 *閱為您的專案設定* SDK。
1. 建立例 `MediaEncrypter` 項。
1. 將加密的檔案傳遞至 `MediaEncrypter.examineEncryptedContent` 傳回物件的方 `KeyMetaData` 法。

1. 檢查對象內的 `KeyMetaData` 資訊。

如需說明如何從加密檔案擷取DRM中繼資料的范常式式碼，請參 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 閱「參考實作命令列工具」 [!DNL samples/] 目錄。
