---
description: 如果選擇HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立pkcs11.cfg配置檔案。
title: HSM配置
exl-id: 4c4423ea-b7af-4a30-99ac-f5b74a1e1168
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# HSM配置{#hsm-configuration}

如果選擇HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立pkcs11.cfg配置檔案。

必須在 *LicenseServer.ConfigRoot* 的子菜單。

查看 [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] PKCS11配置檔案示例。

請參見Sun PKCS11提供程式文檔，其中涉及 [!DNL pkcs11.cfg] 的子菜單。

可以從以下目錄使用以下命令： [!DNL pkcs11.cfg] 檔案所在位置( [!DNL keytool] 已隨Java JRE和JDK一起安裝)，以驗證HSM和Sun PKCS11配置檔案是否已正確配置：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在清單中查看您的憑據，則HSM配置正確，許可證伺服器現在可以訪問憑據。
