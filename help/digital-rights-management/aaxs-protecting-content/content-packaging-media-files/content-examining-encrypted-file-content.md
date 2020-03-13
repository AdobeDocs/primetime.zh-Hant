---
seo-title: 檢查加密的檔案內容
title: 檢查加密的檔案內容
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 檢查加密的檔案內容 {#examining-encrypted-file-content}

要使用Java API檢查FLV或F4V檔案的內容，請執行以下步驟：

1. 設定您的開發環境，並將「設定開發環境」中提 [及的所有JAR檔案包括在項目](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 中。
1. 建立例 `MediaEncrypter` 項。
1. 將加密的檔案傳遞至 `MediaEncrypter.examineEncryptedContent` 傳回物件的方 `KeyMetaData` 法。
1. 檢查對象內的 `KeyMetaData` 資訊。

如需示範如何從加密檔案擷取DRM中繼資料的范常式式碼，請參 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 閱參考實作命令列工具「範例」目錄。
