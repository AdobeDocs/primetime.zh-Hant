---
title: 升級現有部署
description: 升級現有部署
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 升級現有部署{#upgrading-existing-deployments}

若要升級執行3.0版參考實作授權伺服器或Watched Folder Packager的伺服器，請將部署在應用程式伺服器上的[!DNL .war]檔案取代為Adobe存取參考實作伺服器隨附的檔案。

如果您打算使用Reference Implementation License Server的域註冊，則需要幾個新的資料庫表。 要重新建立整個參考實施資料庫，請運行`CreateSampleDB.sql`。 要保留現有資料庫記錄並添加新表，請開啟`CreateSampleDB.sql`並僅運行命令以建立以下表：

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

必須將下列屬性新增至flashaccess-refimpl.properties，才能使用網域支援：

* `HandlerConfiguration.DomainCAs.n` 或  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password`或  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

必須向[!DNL flashaccess-refimpl.properties]添加以下屬性，以支援向iOS客戶端發送遠程密鑰：

* `HandlerConfiguration.KeyServerCertificate` 或  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

