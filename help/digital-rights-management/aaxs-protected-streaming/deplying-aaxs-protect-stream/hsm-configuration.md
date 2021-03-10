---
title: HSM配置
description: HSM配置
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# HSM配置{#hsm-configuration}

如果您選擇使用HSM來儲存伺服器憑據，則必須將私鑰和證書載入到HSM上並建立[!DNL pkcs11.cfg]配置檔案。 此檔案必須位於&#x200B;*LicenseServer.ConfigRoot*&#x200B;目錄中。 有關PKCS11配置檔案示例，請參見Adobe訪問DVD上的[!DNL Adobe Access Server for Protected Streaming/configs]目錄。 有關[!DNL pkcs11.cfg]格式的資訊，請參見Sun PKCS11提供程式文檔。

要驗證HSM和Sun PKCS11配置檔案是否已正確配置，可以從[!DNL pkcs11.cfg]檔案所在的目錄（[!DNL keytool]隨Java JRE和JDK一起安裝）使用以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您在清單中看到您的認證，HSM已正確設定，授權伺服器將可存取認證。

>[!NOTE]
>
>針對受保護串流的Adobe存取伺服器目前不支援64位元Windows作業系統上的HSM。
