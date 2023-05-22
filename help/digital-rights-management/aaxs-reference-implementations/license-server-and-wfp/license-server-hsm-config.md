---
title: HSM配置
description: HSM配置
copied-description: true
exl-id: 0418bcc1-0a85-4074-9616-915f77507bdd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# HSM配置 {#hsm-configuration}

不需要使用HSM，但建議使用。 可以將引用實現配置為使用Sun PKCS11提供程式支援HSM。 要在HSM上使用憑據，必須為Sun PKCS11提供程式建立配置檔案。 有關詳細資訊，請參閱Sun文檔。 要驗證HSM和Sun PKCS11配置檔案是否配置正確，可以使用以下命令（keytool隨Java JDK一起安裝）:

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

如果在清單中看到您的憑據，則HSM配置正確。

>[!NOTE]
>
>從Java 1.7開始，64位Sun Java for Windows不支援AdobeAccess DRM與HSM設備通信所需的PKCS11介面。 如果您計畫使用HSM，請使用32位版本的Java，或使用支援完整PKCS11介面的JDK。
