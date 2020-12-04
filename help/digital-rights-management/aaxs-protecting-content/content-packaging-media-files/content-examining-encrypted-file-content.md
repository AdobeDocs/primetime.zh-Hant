---
seo-title: 檢查加密的檔案內容
title: 檢查加密的檔案內容
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 檢查加密的檔案內容{#examining-encrypted-file-content}

要使用Java API檢查FLV或F4V檔案的內容，請執行以下步驟：

1. 設定您的開發環境並包括[在項目中設定開發環境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)中提及的所有JAR檔案。
1. 建立`MediaEncrypter`實例。
1. 將加密的檔案傳遞到`MediaEncrypter.examineEncryptedContent`方法，該方法返回`KeyMetaData`對象。
1. 檢查`KeyMetaData`對象中的資訊。

如需示範如何從加密檔案擷取DRM中繼資料的范常式式碼，請參閱參考實作命令列工具&quot;samples&quot;目錄中的`com.adobe.flashaccess.samples.mediapackager.ExamineContent`。
