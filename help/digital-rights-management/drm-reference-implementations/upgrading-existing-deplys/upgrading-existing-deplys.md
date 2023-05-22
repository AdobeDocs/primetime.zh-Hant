---
description: 要升級支援3.0版參考實現許可證伺服器或受監視資料夾打包程式的伺服器，需要將部署在應用程式伺服器上的.war檔案替換為Adobe PrimetimeDRM參考實現伺服器中包含的檔案。
title: 升級現有部署
exl-id: 83edaf0a-e527-470d-8b8d-23e5ba86b039
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 概述 {#upgrade-existing-deployments-overview}

要升級支援3.0版參考實現許可證伺服器或受監視資料夾打包程式的伺服器，需要將部署在應用程式伺服器上的.war檔案替換為Adobe PrimetimeDRM參考實現伺服器中包含的檔案。

要在「參考實施許可證伺服器」中使用域註冊，需要幾個新的資料庫表。 您需要重新建立整個引用實現資料庫並運行 `CreateSampleDB.sql`。

要保留資料庫記錄並添加新表，請執行以下操作：

1. 開啟 `CreateSampleDB.sql` 並運行建立以下表的命令：

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. 將以下屬性添加到 [!DNL flashaccess-refimpl.properties] 要使用域支援：

   * `HandlerConfiguration.DomainCAs.n` 或 `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password` 或 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. 將以下屬性添加到 [!DNL flashaccess-refimpl.properties] 支援遠程密鑰傳遞iOS客戶端：

   * `HandlerConfiguration.KeyServerCertificate` 或 `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
