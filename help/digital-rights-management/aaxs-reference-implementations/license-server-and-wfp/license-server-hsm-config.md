---
seo-title: HSM配置
title: HSM配置
uuid: 1cc5be99-c24c-4c1e-9348-fb69f96d8ca5
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# HSM配置{#hsm-configuration}

不需要使用HSM，但建議使用。 可以將參考實現配置為使用Sun PKCS11提供程式支援HSM。 要在HSM上使用憑據，必須為Sun PKCS11提供程式建立配置檔案。 有關詳細資訊，請參見Sun文檔。 要驗證HSM和Sun PKCS11配置檔案是否已正確配置，可以使用以下命令（keytool隨Java JDK一起安裝）:

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

如果您在清單中看到憑據，則HSM已正確配置。

>[!NOTE]
>
>從Java 1.7開始，64位元Sun Java for Windows不支援Adobe Access DRM與HSM裝置通訊所需的PKCS11介面。 如果您打算使用HSM，請使用32位版本的Java，或使用支援完整PKCS11介面的JDK。

