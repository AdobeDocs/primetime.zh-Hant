---
title: 自訂授權擴充功能
description: 在取得授權期間可以叫用自訂授權邏輯，以決定是否應將授權發給要求的用戶端。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 自訂授權擴充功能{#custom-authorization-extensions}

在取得授權期間可以叫用自訂授權邏輯，以決定是否應將授權發給要求的用戶端。

若要實作您自己的客戶授權擴充功能，請先查看位於範例目錄中的[!DNL SampleAuthorizer.java]范常式式碼（此範例的編譯版本位於flashaccess-license-server-ext-sample.jar中）。

若要建立您自己的擴充功能，請實作`com.adobe.flashaccess.server.license.extension.auth.IAuthorizer`介面，並確定`flashaccess-license-server-exts.jar`和`commons-logging.jar`位於建置路徑`adobe-flashaccess-sdk.jar`上，如果您使用`IMessageFacade`中的某些欄位，則也必須位於建置路徑上。 要部署副檔名，請將jar或類檔案複製到&#x200B;*LicenseServer.ConfigRoot* `/flashaccessserver/libs`。 如果需要更新jar或類檔案，則必須在使用更新版本之前重新啟動伺服器。 您也必須將授權者類別名稱新增至租用戶設定檔案。
