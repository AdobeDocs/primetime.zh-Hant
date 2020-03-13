---
description: 如果選擇HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立pkcs11.cfg配置檔案。
seo-description: 如果選擇HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立pkcs11.cfg配置檔案。
seo-title: HSM配置
title: HSM配置
uuid: 3610840b-082e-4a73-8aa5-5065f9232e0b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# HSM配置{#hsm-configuration}

如果選擇HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立pkcs11.cfg配置檔案。

必須在 *LicenseServer.ConfigRoot目錄中找到配置檔案* 。

如需 [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] 範例PKCS11設定檔案，請參閱Adobe Primetime DRM DVD上的目錄。

請參見Sun PKCS11提供程式文檔，其中介紹了檔案 [!DNL pkcs11.cfg] 格式。

可以從檔案所在的目錄(隨 [!DNL pkcs11.cfg][!DNL keytool] Java JRE和JDK一起安裝)使用以下命令來驗證HSM和Sun PKCS11配置檔案是否已正確配置：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在清單中查看憑據，則HSM已正確配置，許可證伺服器現在可以訪問憑據。
