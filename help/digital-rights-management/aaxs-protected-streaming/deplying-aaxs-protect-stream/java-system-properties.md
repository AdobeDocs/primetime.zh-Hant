---
title: Java系統屬性
description: Java系統屬性
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Java系統屬性 {#java-system-properties}

下列兩個Java系統屬性可選擇性設定，以修改許可證伺服器的組態和記錄檔位置：

* *LicenseServer.ConfigRoot*  — 包含許可證伺服器的所有組態檔案的目錄。 如需這些檔案內容的詳細資訊，請參閱&quot;[授權伺服器組態檔](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)「。 如果未設定，預設值為 *CATALINA_BASE/licenseserver*.
* *LicenseServer.LogRoot* — 「logs」資料夾的目錄，許可證伺服器應用程式記錄會寫入此目錄。 如果未設定，預設值為 *LicenseServer.ConfigRoot*.

如果您使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 若要啟動Tomcat，可以使用輕鬆設定這些System屬性 `JAVA_OPTS` 環境變數。 啟動Tomcat時，將使用此處設定的任何Java選項。 例如，設定：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
