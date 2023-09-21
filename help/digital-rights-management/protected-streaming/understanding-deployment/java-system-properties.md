---
description: 您可以在許可證伺服器上設定數個Java系統屬性，以控制組態和記錄檔的位置。
title: Java系統屬性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Java系統屬性{#java-system-properties}

您可以在許可證伺服器上設定數個Java系統屬性，以控制組態和記錄檔的位置。

您可以選擇設定下列Java系統屬性：

* *`LicenseServer.ConfigRoot`*  — 包含許可證伺服器組態檔案的目錄名稱。

  另請參閱 *授權伺服器組態檔* 這些檔案內容的詳細資訊。 若未設定，預設值為 `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot*  — 的名稱 [!DNL logs] license server應用程式記錄所在的目錄。 如果您尚未修改此目錄的名稱，則會將此目錄名稱設定為 *LicenseServer.ConfigRoot* 依預設。

如果您使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 檔案啟動Tomcat時，您可以使用 `JAVA_OPTS` 環境變數。 您設定的任何Java選項都會在Tomcat啟動時自動套用。

例如，您可以設定 `JAVA_OPTS` 環境變數，如下所示：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
