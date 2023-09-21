---
title: 正在檢查加密的檔案內容
description: 正在檢查加密的檔案內容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 正在檢查加密的檔案內容 {#examining-encrypted-file-content}

若要使用Java API檢查FLV或F4V檔案的內容，請執行下列步驟：

1. 設定您的開發環境，並包含中提到的所有JAR檔案 [設定開發環境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 在您的專案中。
1. 建立 `MediaEncrypter` 執行個體。
1. 將加密檔案傳遞至 `MediaEncrypter.examineEncryptedContent` 方法，會傳回 `KeyMetaData` 物件。
1. Inspect中的資訊 `KeyMetaData` 物件。

如需示範如何從加密檔案擷取DRM中繼資料的範常式式碼，請參閱 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 在「參考實作」命令列工具「範例」目錄中。
