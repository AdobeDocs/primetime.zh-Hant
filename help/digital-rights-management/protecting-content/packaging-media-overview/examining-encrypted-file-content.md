---
title: 檢查加密的檔案內容
description: 檢查加密的檔案內容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 檢查加密的檔案內容{#examining-encrypted-file-content}

您可以使用Java API檢查加密媒體檔案的內容。

要檢查加密的檔案內容：

1. 設定您的開發環境並包括所有JAR檔案。 請參閱&#x200B;*設定專案的SDK*。
1. 建立`MediaEncrypter`實例。
1. 將加密的檔案傳遞到`MediaEncrypter.examineEncryptedContent`方法，該方法返回`KeyMetaData`對象。

1. Inspect`KeyMetaData`對象中的資訊。

有關說明如何從加密檔案提取DRM元資料的示例代碼，請參見Reference Implementation Command Line Tools [!DNL samples/]目錄中的`com.adobe.flashaccess.samples.mediapackager.ExamineContent`。
