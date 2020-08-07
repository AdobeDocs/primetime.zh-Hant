---
description: 可以使用支援HSM的Sun PKCS#11提供程式配置參考實現。 雖然不需要使用HSM，但建議使用。
seo-description: 可以使用支援HSM的Sun PKCS#11提供程式配置參考實現。 雖然不需要使用HSM，但建議使用。
seo-title: HSM配置
title: HSM配置
uuid: 2741ac40-aa42-4aa7-9864-037f3ed3dee2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# HSM配置{#hsm-configuration}

可以使用支援HSM的Sun PKCS#11提供程式配置參考實現。 雖然不需要使用HSM，但建議使用。

要在HSM上使用憑據，必須為Sun PKCS#11提供程式建立配置檔案。 有關詳細資訊，請參 [閱《Java PCKS#11參考指南》](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html)。

要驗證是否配置了HSM和Sun PKCS#11配置檔案，請使用隨Java JDK安裝的keytool鍵入以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果可以在清單中查看憑據，則已正確配置了HSM。

>[!NOTE]
>
>自Java 1.7起，64位元Sun Java for Windows不再支援Adobe Primetime DRM與HSM裝置通訊所需的PKCS#11介面。 如果您打算使用HSM，請確定您使用32位元版本的Java，或使用支援完整PKCS#11介面的JDK。

