---
description: 若要升級支援3.0版參考實作授權伺服器或Watched Folder Packager的伺服器，您必須將部署在應用程式伺服器上的。war檔案取代為Adobe Primetime DRM參考實作伺服器所包含的檔案。
seo-description: 若要升級支援3.0版參考實作授權伺服器或Watched Folder Packager的伺服器，您必須將部署在應用程式伺服器上的。war檔案取代為Adobe Primetime DRM參考實作伺服器所包含的檔案。
seo-title: 升級現有部署
title: 升級現有部署
uuid: 1a40aae9-f639-41fa-b42d-cf8cdfcde694
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# 概述{#upgrade-existing-deployments-overview}

若要升級支援3.0版參考實作授權伺服器或Watched Folder Packager的伺服器，您必須將部署在應用程式伺服器上的。war檔案取代為Adobe Primetime DRM參考實作伺服器所包含的檔案。

要使用參考實施許可證伺服器的域註冊，需要幾個新的資料庫表。 您需要重新建立整個參考實施資料庫並運行`CreateSampleDB.sql`。

要保留資料庫記錄並添加新表：

1. 開啟`CreateSampleDB.sql`並運行建立以下表的命令：

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. 將以下屬性添加到[!DNL flashaccess-refimpl.properties]以使用域支援：

   * `HandlerConfiguration.DomainCAs.n` 或  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password` 或  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. 將下列屬性新增至[!DNL flashaccess-refimpl.properties]，以支援將遠端金鑰傳送至iOS用戶端：

   * `HandlerConfiguration.KeyServerCertificate` 或  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`