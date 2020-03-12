---
description: 您可在授權伺服器上設定數個Java系統屬性，以控制組態和記錄檔的位置。
seo-description: 您可在授權伺服器上設定數個Java系統屬性，以控制組態和記錄檔的位置。
seo-title: Java系統屬性
title: Java系統屬性
uuid: d8c72359-bf61-47e0-9cd5-b21225d5fe49
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Java系統屬性{#java-system-properties}

您可在授權伺服器上設定數個Java系統屬性，以控制組態和記錄檔的位置。

您可以選擇性地配置以下Java系統屬性：

* *`LicenseServer.ConfigRoot`* — 包含許可證伺服器配置檔案的目錄的名稱。

   如需 *這些檔案內容的詳細資訊* ，請參閱授權伺服器設定檔。 如果未配置，則預設值為 `CATALINA_BASE/licenseserver`。

* *LicenseServer.LogRoot* — 許可證服 [!DNL logs] 務器應用程式日誌所在的目錄的名稱。 如果您尚未修改此目錄的名稱，則此目錄的名稱將預設配置 *為LicenseServer.ConfigRoot* 。

如果使用或文 [!DNL catalina.bat] 件啟 [!DNL catalina.sh] 動Tomcat，則可以使用環境變數配置系統 `JAVA_OPTS` 屬性。 在Tomcat啟動時，您所配置的任何Java選項都會自動套用。

例如，您可以按如下方 `JAVA_OPTS` 式配置環境變數：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

