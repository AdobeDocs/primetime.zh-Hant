---
description: 若要升級支援3.0版Reference Implementation License Server或Watched Folder Packager的伺服器，您必須以Adobe Primetime DRM Reference Implementation Server隨附的檔案，取代已部署在應用程式伺服器上的.war檔案。
title: 升級現有部署
exl-id: 83edaf0a-e527-470d-8b8d-23e5ba86b039
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 概觀 {#upgrade-existing-deployments-overview}

若要升級支援3.0版Reference Implementation License Server或Watched Folder Packager的伺服器，您必須以Adobe Primetime DRM Reference Implementation Server隨附的檔案，取代已部署在應用程式伺服器上的.war檔案。

若要使用Reference Implementation License Server進行網域註冊，則需要幾個新的資料庫表格。 您需要重新建立整個參考實作資料庫並執行 `CreateSampleDB.sql`.

若要保留資料庫記錄並新增表格：

1. 開啟 `CreateSampleDB.sql` 並執行建立下清單格的命令：

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. 將下列屬性新增至 [!DNL flashaccess-refimpl.properties] 使用網域支援：

   * `HandlerConfiguration.DomainCAs.n` 或 `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password` 或 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. 將下列屬性新增至 [!DNL flashaccess-refimpl.properties] 若要支援將遠端金鑰傳遞至iOS使用者端：

   * `HandlerConfiguration.KeyServerCertificate` 或 `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
