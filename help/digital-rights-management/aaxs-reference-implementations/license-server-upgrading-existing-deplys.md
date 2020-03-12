---
seo-title: 升級現有部署
title: 升級現有部署
uuid: 57e62a88-e541-435c-8274-7f1602548601
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 升級現有部署 {#upgrading-existing-deployments}

若要升級執行3.0版參考實作授權伺服器或Watched Folder Packager的伺服器，請將部署在應用程式伺服器上的檔案取代為Adobe Access Reference Implementation Server隨附的檔案。 [!DNL .war]

如果您打算使用Reference Implementation License Server的域註冊，則需要幾個新的資料庫表。 要重新建立整個參考實施資料庫，請運行 `CreateSampleDB.sql`。 要保留現有資料庫記錄並添加新表，請打 `CreateSampleDB.sql`開並僅運行命令以建立以下表：

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

必須將下列屬性新增至flashaccess-refimpl.properties，才能使用網域支援：

* `HandlerConfiguration.DomainCAs.n` 或 `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password`或 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

必須新增下列屬性，才 [!DNL flashaccess-refimpl.properties] 能支援遠端金鑰傳送至iOS用戶端：

* `HandlerConfiguration.KeyServerCertificate` 或 `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

