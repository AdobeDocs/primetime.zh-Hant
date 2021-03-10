---
description: 您可在授權伺服器上設定數個Java系統屬性，以控制設定和記錄檔的位置。
title: Java系統屬性
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Java系統屬性{#java-system-properties}

您可在授權伺服器上設定數個Java系統屬性，以控制設定和記錄檔的位置。

您可以選擇性地配置以下Java系統屬性：

* *`LicenseServer.ConfigRoot`* — 包含許可證伺服器配置檔案的目錄的名稱。

   有關這些檔案內容的詳細資訊，請參見&#x200B;*許可證伺服器配置檔案*。 如果未配置，則預設值為`CATALINA_BASE/licenseserver`。

* *LicenseServer.LogRoot* — 許可證服 [!DNL logs] 務器應用程式日誌所在的目錄的名稱。如果您未修改此目錄的名稱，則預設情況下，此目錄的名稱配置為&#x200B;*LicenseServer.ConfigRoot*。

如果使用[!DNL catalina.bat]或[!DNL catalina.sh]檔案啟動Tomcat，則可以使用`JAVA_OPTS`環境變數配置系統屬性。 在Tomcat啟動時，您所配置的任何Java選項都會自動套用。

例如，您可以按如下方式配置`JAVA_OPTS`環境變數：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

