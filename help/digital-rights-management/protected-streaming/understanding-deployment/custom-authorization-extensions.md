---
description: 您可以在取得授權期間叫用自訂授權邏輯，以決定是否應將授權發給要求的用戶端。
seo-description: 您可以在取得授權期間叫用自訂授權邏輯，以決定是否應將授權發給要求的用戶端。
seo-title: 自訂授權擴充功能
title: 自訂授權擴充功能
uuid: 588b05e5-3402-4586-bbd4-58b7e9a58ee4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 自訂授權擴充功能{#custom-authorization-extensions}

您可以在取得授權期間叫用自訂授權邏輯，以決定是否應將授權發給要求的用戶端。

如果您想要實作自己的客戶授權擴充功能，您必須先查看位於 [!DNL SampleAuthorizer.java] samples目錄中的范常式式碼。 此示例的編譯版本位於 [!DNL flashaccess-license-server-ext-sample.jar]。

如果您想要建立自己的擴充功能，則需要實作介面，並確 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 定 [!DNL flashaccess-license-server-exts.jar][!DNL commons-logging.jar] 並位於建置路徑中(如果您使用中的特定欄位，也必須位於建置路徑中 [!DNL adobe-flashaccess-sdk.jar]`IMessageFacade`)。

如果要部署副檔名，需要將jar或類檔案複製到 *LicenseServer.ConfigRoot*[!DNL /flashaccessserver/libs]。

如果要更新jar或類檔案，則需要在使用更新版本之前重新啟動伺服器。 您也必須將授權者類別名稱新增至租用戶設定檔案。
