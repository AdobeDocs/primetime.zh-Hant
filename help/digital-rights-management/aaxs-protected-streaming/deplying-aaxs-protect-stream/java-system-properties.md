---
seo-title: Java系統屬性
title: Java系統屬性
uuid: ad1f3d9b-7d95-4e19-a0f8-fd7d4dd4dc32
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Java系統屬性 {#java-system-properties}

可以選擇設定以下兩個Java系統屬性來修改許可證伺服器的配置和日誌檔案的位置：

* *LicenseServer.ConfigRoot* — 包含許可證伺服器的所有配置檔案的目錄。 如需這些檔案內容的詳細資訊，請參閱「授[權伺服器設定檔](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)」。 如果未設定，則預設值為 *CATALINA_BASE/licenseserver*。
* *LicenseServer.LogRoot* — 「日誌」資料夾的目錄，其中寫入了許可證伺服器應用程式日誌。 如果未設定，則預設值 *為LicenseServer.ConfigRoot*。

如果使用或 [!DNL catalina.bat] 啟 [!DNL catalina.sh] 動Tomcat，可使用環境變數輕鬆設定這些系統 `JAVA_OPTS` 屬性。 在啟動Tomcat時，將使用此處設定的任何Java選項。 例如，設定：

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

