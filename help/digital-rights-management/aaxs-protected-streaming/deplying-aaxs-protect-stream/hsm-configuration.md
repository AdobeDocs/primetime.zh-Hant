---
title: HSM配置
description: HSM配置
copied-description: true
exl-id: a3e5759e-1419-4519-bcd7-de83364a48f8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# HSM配置 {#hsm-configuration}

如果您選擇使用HSM儲存伺服器憑據，則必須將私鑰和證書載入到HSM並建立 [!DNL pkcs11.cfg] 配置檔案。 此檔案必須位於 *LicenseServer.ConfigRoot* 的子菜單。 查看 [!DNL Adobe Access Server for Protected Streaming/configs] Adobe訪問DVD上的目錄（例如PKCS11配置檔案）。 有關格式的資訊 [!DNL pkcs11.cfg]，請參見Sun PKCS11提供程式文檔。

要驗證HSM和Sun PKCS11配置檔案是否配置正確，可以使用以下命令： [!DNL pkcs11.cfg] 檔案所在位置( [!DNL keytool] 隨Java JRE和JDK一起安裝):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果在清單中看到您的憑據，則HSM配置正確，許可證伺服器將能夠訪問憑據。

>[!NOTE]
>
>Adobe訪問伺服器受保護的流目前不支援64位Windows作業系統上的HSM。
