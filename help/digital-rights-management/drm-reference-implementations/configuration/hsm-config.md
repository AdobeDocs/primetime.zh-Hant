---
description: 您可以使用支援HSM的Sun PKCS#11提供者來設定參照實作。 雖然不要求使用HSM，但建議使用。
title: HSM組態
exl-id: 87a7d242-8202-4749-91a6-e6697be6a61d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# HSM組態{#hsm-configuration}

您可以使用支援HSM的Sun PKCS#11提供者來設定參照實作。 雖然不要求使用HSM，但建議使用。

若要在HSM上使用認證，您必須為Sun PKCS#11提供者建立組態檔。 如需詳細資訊，請參閱 [Java PCKS#11參考指南](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

若要確認您的HSM和Sun PKCS#11組態檔已設定，請使用隨Java JDK安裝的keytool鍵入以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在清單中檢視您的認證，表示您已正確設定HSM。

>[!NOTE]
>
>自Java 1.7起，適用於Windows的64位元Sun Java不再支援Adobe Primetime DRM與HSM裝置通訊所需的PKCS#11介面。 如果您打算使用HSM，請確定您使用的是32位元版Java，或使用支援完整PKCS#11介面的JDK。
