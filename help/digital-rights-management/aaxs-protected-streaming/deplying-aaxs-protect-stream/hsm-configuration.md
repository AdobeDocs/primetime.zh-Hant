---
seo-title: HSM配置
title: HSM配置
uuid: da4d7118-65a8-460d-a796-b7bf5c28b208
translation-type: tm+mt
source-git-commit: ac75f63f98060e1937570476362bb5d4458d1f85

---


# HSM配置 {#hsm-configuration}

如果您選擇使用HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM上並建立配 [!DNL pkcs11.cfg] 置檔案。 此檔案必須位於 *LicenseServer.ConfigRoot目錄中* 。 如需PKCS11 [!DNL Adobe Access Server for Protected Streaming/configs] 組態檔的範例，請參閱Adobe Access DVD上的目錄。 有關格式的資訊 [!DNL pkcs11.cfg]，請參見Sun PKCS11提供程式文檔。

要驗證HSM和Sun PKCS11配置檔案是否已正確配置，可以從檔案所在的目錄（隨Java JRE和JDK一起安裝）中使用 [!DNL pkcs11.cfg][!DNL keytool] 以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您在清單中看到您的認證，HSM已正確設定，授權伺服器將可存取認證。

>[!NOTE]
>
>Adobe Access Server for Protected Streaming目前不支援64位元Windows作業系統上的HSM。
