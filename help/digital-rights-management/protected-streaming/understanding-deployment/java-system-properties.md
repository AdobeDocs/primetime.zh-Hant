---
description: 可以在許可證伺服器上配置幾個Java系統屬性，以控制配置和日誌檔案的位置。
title: Java系統屬性
exl-id: 08fe6910-9d58-41c3-91d3-514406bedf05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Java系統屬性{#java-system-properties}

可以在許可證伺服器上配置幾個Java系統屬性，以控制配置和日誌檔案的位置。

您可以選擇配置以下Java系統屬性：

* *`LicenseServer.ConfigRoot`*  — 包含許可證伺服器配置檔案的目錄名稱。

   請參閱 *許可證伺服器配置檔案* 的子菜單。 如果未配置，則預設值為 `CATALINA_BASE/licenseserver`。

* *LicenseServer.LogRoot*  — 名稱 [!DNL logs] 許可證伺服器應用程式日誌所在的目錄。 如果尚未修改此目錄的名稱，則此目錄的名稱將配置為 *LicenseServer.ConfigRoot* 預設值。

如果使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 檔案以啟動Tomcat，可以使用 `JAVA_OPTS` 環境變數。 在Tomcat啟動時，將自動應用您配置的任何Java選項。

例如，您可以配置 `JAVA_OPTS` 環境變數如下：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
