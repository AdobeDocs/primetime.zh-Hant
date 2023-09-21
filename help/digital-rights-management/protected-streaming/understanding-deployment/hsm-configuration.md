---
description: 如果您選取HSM來儲存伺服器認證，則必須將私密金鑰和憑證載入HSM並建立pkcs11.cfg組態檔。
title: HSM組態
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# HSM組態{#hsm-configuration}

如果您選取HSM來儲存伺服器認證，則必須將私密金鑰和憑證載入HSM並建立pkcs11.cfg組態檔。

您必須在以下位置找到組態檔： *LicenseServer.ConfigRoot* 目錄。

請參閱 [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] Adobe Primetime DRM DVD上的目錄，例如PKCS11組態檔。

請參閱Sun PKCS11提供者檔案，瞭解 [!DNL pkcs11.cfg] 檔案。

您可以從目錄中使用以下指令，其中 [!DNL pkcs11.cfg] 檔案位於( [!DNL keytool] Java JRE和JDK一起安裝)，以驗證HSM和Sun PKCS11組態檔是否已正確設定：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在清單中檢視您的認證，則HSM已正確設定，且授權伺服器現在可以存取認證。
