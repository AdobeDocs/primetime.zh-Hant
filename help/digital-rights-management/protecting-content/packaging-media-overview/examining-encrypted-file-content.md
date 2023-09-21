---
title: 正在檢查加密的檔案內容
description: 正在檢查加密的檔案內容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 正在檢查加密的檔案內容{#examining-encrypted-file-content}

您可以使用Java API來檢查加密媒體檔案的內容。

檢查加密的檔案內容：

1. 設定您的開發環境，並包含所有JAR檔案。 另請參閱 *設定SDK* 專案的。
1. 建立 `MediaEncrypter` 執行個體。
1. 將加密檔案傳遞至 `MediaEncrypter.examineEncryptedContent` 方法，會傳回 `KeyMetaData` 物件。

1. Inspect中的資訊 `KeyMetaData` 物件。

如需說明如何從加密檔案擷取DRM中繼資料的範常式式碼，請參閱 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 在參照實作命令列工具中 [!DNL samples/] 目錄。
