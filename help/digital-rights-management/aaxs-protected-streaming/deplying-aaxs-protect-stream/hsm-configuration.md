---
title: HSM組態
description: HSM組態
copied-description: true
exl-id: a3e5759e-1419-4519-bcd7-de83364a48f8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# HSM組態 {#hsm-configuration}

如果您選擇使用HSM來儲存伺服器認證，則必須將私密金鑰和憑證載入到HSM上，並建立 [!DNL pkcs11.cfg] 設定檔。 此檔案必須位於 *LicenseServer.ConfigRoot* 目錄。 請參閱 [!DNL Adobe Access Server for Protected Streaming/configs] Adobe存取DVD上的目錄，例如PKCS11組態檔。 如需格式化的詳細資訊， [!DNL pkcs11.cfg]請參閱Sun PKCS11提供者檔案。

若要確認您的HSM和Sun PKCS11組態檔已正確設定，您可以使用以下目錄中的命令： [!DNL pkcs11.cfg] 檔案位於( [!DNL keytool] 隨Java JRE和JDK一起安裝)：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您在清單中看到您的認證，則HSM已正確設定，且授權伺服器將能夠存取認證。

>[!NOTE]
>
>受保護串流的Adobe存取伺服器目前不支援64位元Windows作業系統上的HSM。
