---
title: 正在檢查加密的檔案內容
description: 正在檢查加密的檔案內容
copied-description: true
exl-id: df1fd04d-016e-4770-bcb9-97bfe2d39260
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 正在檢查加密的檔案內容{#examining-encrypted-file-content}

可以使用Java API檢查加密媒體檔案的內容。

要檢查加密的檔案內容：

1. 設定開發環境並包括所有JAR檔案。 請參閱 *設定SDK* 為你的項目。
1. 建立 `MediaEncrypter` 實例。
1. 將加密的檔案傳遞到 `MediaEncrypter.examineEncryptedContent` 方法，它返回 `KeyMetaData` 的雙曲餘切值。

1. Inspect `KeyMetaData` 的雙曲餘切值。

有關描述如何從加密檔案中提取DRM元資料的示例代碼，請參見 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 在「參考實現」命令行工具中 [!DNL samples/] 的子菜單。
