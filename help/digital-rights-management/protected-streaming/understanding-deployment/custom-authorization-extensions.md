---
description: 您可以在取得授權期間叫用自訂授權邏輯，以決定是否應將授權發給要求的用戶端。
title: 自訂授權擴充功能
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# 自訂授權擴充功能{#custom-authorization-extensions}

您可以在取得授權期間叫用自訂授權邏輯，以決定是否應將授權發給要求的用戶端。

如果您想要實作自己的客戶授權擴充功能，您必須先查看位於範例目錄中的[!DNL SampleAuthorizer.java]范常式式碼。 此示例的編譯版本位於[!DNL flashaccess-license-server-ext-sample.jar]中。

如果要構建自己的擴展，您需要實施`com.adobe.flashaccess.server.license.extension.auth.IAuthorizer`介面，並確保[!DNL flashaccess-license-server-exts.jar]和[!DNL commons-logging.jar]位於構建路徑中（如果使用`IMessageFacade`中的某些欄位，[!DNL adobe-flashaccess-sdk.jar]也必須位於構建路徑中）。

如果要部署副檔名，需要將jar或類檔案複製到&#x200B;*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs]。

如果要更新jar或類檔案，則需要在使用更新版本之前重新啟動伺服器。 您也必須將授權者類別名稱新增至租用戶設定檔案。
