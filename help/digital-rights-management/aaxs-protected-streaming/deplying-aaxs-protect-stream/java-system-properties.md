---
title: Java系統屬性
description: Java系統屬性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Java系統屬性{#java-system-properties}

可以選擇設定以下兩個Java系統屬性來修改許可證伺服器的配置和日誌檔案的位置：

* *LicenseServer.ConfigRoot* — 包含許可證伺服器的所有配置檔案的目錄。有關這些檔案內容的詳細資訊，請參閱「[許可證伺服器配置檔案](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)」。 如果未設定，則預設值為&#x200B;*CATALINA_BASE/licenseserver*。
* *LicenseServer.LogRoot* — 「日誌」資料夾的目錄，其中寫入了許可證伺服器應用程式日誌。如果未設定，則預設值為&#x200B;*LicenseServer.ConfigRoot*。

如果使用[!DNL catalina.bat]或[!DNL catalina.sh]啟動Tomcat，則可以使用`JAVA_OPTS`環境變數輕鬆設定這些系統屬性。 在啟動Tomcat時，將使用此處設定的任何Java選項。 例如，設定：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

