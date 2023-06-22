---
title: 自訂授權延伸
description: 在授權取得期間可叫用自訂授權邏輯，以決定是否應將授權核發給請求使用者端。
exl-id: bf7870f5-11bf-4392-a422-506b47d684f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 自訂授權延伸 {#custom-authorization-extensions}

在授權取得期間可叫用自訂授權邏輯，以決定是否應將授權核發給請求使用者端。

若要實作您自己的客戶授權擴充功能，請先檢視 [!DNL SampleAuthorizer.java] 範常式式碼位於samples目錄中（此範例的編譯版本位於flashaccess-license-server-ext-sample.jar）。

若要建立自己的擴充功能，請實作 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 介面並確認 `flashaccess-license-server-exts.jar` 和 `commons-logging.jar` 在建置路徑上 `adobe-flashaccess-sdk.jar` 如果您使用的某些欄位，也必須位於建置路徑上 `IMessageFacade`)。 若要部署擴充功能，請將jar或類別檔案複製到 *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. 如果您需要更新jar或class檔案，則必須先重新啟動伺服器，才能使用更新的版本。 您也必須將授權者類別名稱新增至租使用者設定檔。
