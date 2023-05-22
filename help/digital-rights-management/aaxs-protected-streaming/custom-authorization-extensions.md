---
title: 自定義授權擴展
description: 在許可獲取期間可以調用自定義授權邏輯以確定是否應向請求的客戶端頒發許可。
exl-id: bf7870f5-11bf-4392-a422-506b47d684f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 自定義授權擴展 {#custom-authorization-extensions}

在許可獲取期間可以調用自定義授權邏輯以確定是否應向請求的客戶端頒發許可。

要實施您自己的客戶授權擴展，請首先查看 [!DNL SampleAuthorizer.java] 示例代碼位於samples目錄（此示例的編譯版本位於flashaccess-license-server-ext-sample.jar中）。

要構建自己的擴展，請實施 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 介面，確保 `flashaccess-license-server-exts.jar` 和 `commons-logging.jar` 在生成路徑上 `adobe-flashaccess-sdk.jar` 如果在中使用某些欄位，則還必須位於生成路徑上 `IMessageFacade`)。 要部署副檔名，請將jar或類檔案複製到 *LicenseServer.ConfigRoot* `/flashaccessserver/libs`。 如果需要更新jar或類檔案，則必須在使用更新的版本之前重新啟動伺服器。 還必須將授權器類名添加到租戶配置檔案。
