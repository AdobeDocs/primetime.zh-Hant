---
title: 正在檢查加密的檔案內容
description: 正在檢查加密的檔案內容
copied-description: true
exl-id: a8a61d1c-c259-4346-9a71-6741f70697ae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 正在檢查加密的檔案內容 {#examining-encrypted-file-content}

要使用Java API檢查FLV或F4V檔案的內容，請執行以下步驟：

1. 設定開發環境並包括中提及的所有JAR檔案 [建立開發環境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 你的項目。
1. 建立 `MediaEncrypter` 實例。
1. 將加密的檔案傳遞到 `MediaEncrypter.examineEncryptedContent` 方法，它返回 `KeyMetaData` 的雙曲餘切值。
1. Inspect `KeyMetaData` 的雙曲餘切值。

有關演示如何從加密檔案中提取DRM元資料的示例代碼，請參見 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 在「參考實現」命令行工具「示例」目錄中。
