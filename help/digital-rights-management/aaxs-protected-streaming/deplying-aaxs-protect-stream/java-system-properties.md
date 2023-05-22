---
title: Java系統屬性
description: Java系統屬性
copied-description: true
exl-id: 3fac8fac-7c71-4638-a671-eecc203dc871
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Java系統屬性 {#java-system-properties}

可以選擇設定以下兩個Java系統屬性以修改許可證伺服器的配置和日誌檔案的位置：

* *LicenseServer.ConfigRoot*  — 包含許可證伺服器的所有配置檔案的目錄。 有關這些檔案內容的詳細資訊，請參閱[許可證伺服器配置檔案](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)。 如果未設定，則預設值為 *CATALINA_BASE/許可伺服器*。
* *LicenseServer.LogRoot*  — 寫入許可證伺服器應用程式日誌的「logs」資料夾的目錄。 如果未設定，則預設值為 *LicenseServer.ConfigRoot*。

如果您使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 要啟動Tomcat，可以使用 `JAVA_OPTS` 環境變數。 啟動Tomcat時，將使用此處設定的任何Java選項。 例如，設定：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
