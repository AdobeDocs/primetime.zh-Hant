---
description: 您可以在獲取許可證期間調用自定義授權邏輯，以確定是否應向請求的客戶端頒發許可證。
title: 自定義授權擴展
exl-id: dbdda9c6-32bf-4904-981f-0029bf0a82f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# 自定義授權擴展{#custom-authorization-extensions}

您可以在獲取許可證期間調用自定義授權邏輯，以確定是否應向請求的客戶端頒發許可證。

如果要實施您自己的客戶授權擴展，您必須首先查看 [!DNL SampleAuthorizer.java] 位於示例目錄中的示例代碼。 此示例的編譯版本位於 [!DNL flashaccess-license-server-ext-sample.jar]。

如果要構建自己的擴展，則需要實施 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 介面，確保 [!DNL flashaccess-license-server-exts.jar] 和 [!DNL commons-logging.jar] 位於生成路徑( [!DNL adobe-flashaccess-sdk.jar] 如果在中使用某些欄位，則還必須位於生成路徑中 `IMessageFacade`)。

如果要部署副檔名，需要將jar或類檔案複製到 *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs]。

如果要更新jar或類檔案，則需要先重新啟動伺服器，然後才能使用更新的版本。 還必須將授權器類名添加到租戶配置檔案。
