---
title: 升級現有部署
description: 升級現有部署
copied-description: true
exl-id: e07b883f-d5f7-40d3-9221-a0dc2d859a5a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 升級現有部署 {#upgrading-existing-deployments}

若要升級執行3.0版參考實作授權伺服器或Watched Folder Packager的伺服器，請將 [!DNL .war] 使用Adobe存取參考實作伺服器隨附的檔案部署在應用程式伺服器上的檔案。

如果您打算使用參照實作授權伺服器的網域註冊，則需要幾個新的資料庫表格。 若要重新建立整個參考實作資料庫，請執行 `CreateSampleDB.sql`. 若要保留現有資料庫記錄並新增表格，請開啟 `CreateSampleDB.sql`並且只執行命令以建立下清單格：

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

下列屬性必須新增至flashaccess-refimpl.properties才能使用網域支援：

* `HandlerConfiguration.DomainCAs.n` 或 `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password`，或 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

下列屬性必須新增至 [!DNL flashaccess-refimpl.properties] 若要支援將遠端金鑰傳遞至iOS使用者端：

* `HandlerConfiguration.KeyServerCertificate` 或 `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
