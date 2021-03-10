---
description: 如果選擇HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立pkcs11.cfg配置檔案。
title: HSM配置
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# HSM配置{#hsm-configuration}

如果選擇HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立pkcs11.cfg配置檔案。

必須在&#x200B;*LicenseServer.ConfigRoot*&#x200B;目錄中找到配置檔案。

有關PKCS11配置檔案示例，請參見Adobe PrimetimeDRM DVD上的[!DNL Adobe Primetime DRM Server for Protected Streaming/configs]目錄。

有關[!DNL pkcs11.cfg]檔案的格式，請參見Sun PKCS11提供程式文檔。

可以從[!DNL pkcs11.cfg]檔案所在的目錄（[!DNL keytool]隨Java JRE和JDK一起安裝）使用以下命令來驗證HSM和Sun PKCS11配置檔案是否已正確配置：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在清單中查看憑據，則HSM已正確配置，許可證伺服器現在可以訪問憑據。
