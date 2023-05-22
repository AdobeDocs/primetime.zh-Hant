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

要升級運行3.0版參考實施許可證伺服器或受監視資料夾打包程式的伺服器，請替換 [!DNL .war] 部署在Application Server上的檔案，其中包含Adobe訪問參考實施伺服器中的檔案。

如果您計畫使用引用實施許可證伺服器的域註冊，則需要幾個新的資料庫表。 要重新建立整個引用實現資料庫，請運行 `CreateSampleDB.sql`。 要保留現有資料庫記錄並添加新表，請開啟 `CreateSampleDB.sql`並僅運行命令以建立以下表：

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

必須將以下屬性添加到flashaccess-refimpl.properties中才能使用域支援：

* `HandlerConfiguration.DomainCAs.n` 或 `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password`或 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

必須將以下屬性添加到 [!DNL flashaccess-refimpl.properties] 支援遠程密鑰傳遞iOS客戶端：

* `HandlerConfiguration.KeyServerCertificate` 或 `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
