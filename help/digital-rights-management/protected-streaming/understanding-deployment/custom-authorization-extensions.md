---
description: 您可以在授權取得期間叫用自訂授權邏輯，以決定是否應將授權核發給提出請求的使用者端。
title: 自訂授權延伸
exl-id: dbdda9c6-32bf-4904-981f-0029bf0a82f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# 自訂授權延伸{#custom-authorization-extensions}

您可以在授權取得期間叫用自訂授權邏輯，以決定是否應將授權核發給提出請求的使用者端。

如果您想要實作自己的客戶授權擴充功能，必須先檢視 [!DNL SampleAuthorizer.java] 位於samples目錄中的範常式式碼。 此範例的編譯版本位於 [!DNL flashaccess-license-server-ext-sample.jar].

如果您想要建立自己的擴充功能，必須實作 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 介面並確認 [!DNL flashaccess-license-server-exts.jar] 和 [!DNL commons-logging.jar] 在建置路徑中( [!DNL adobe-flashaccess-sdk.jar] 如果您使用的某些欄位，也必須位於建置路徑中 `IMessageFacade`)。

如果要部署擴充功能，您需要將jar或類別檔案複製到 *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

如果要更新jar或class檔案，您需要先重新啟動伺服器，才能使用更新的版本。 您也必須將授權者類別名稱新增至租使用者設定檔。
