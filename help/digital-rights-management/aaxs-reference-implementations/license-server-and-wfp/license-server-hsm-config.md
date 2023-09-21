---
title: HSM組態
description: HSM組態
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# HSM組態 {#hsm-configuration}

不一定要使用HSM，但建議使用。 參考實作可設定為使用Sun PKCS11提供者提供HSM支援。 若要在HSM上使用認證，您必須為Sun PKCS11提供者建立組態檔。 如需詳細資訊，請參閱Sun檔案。 若要確認您的HSM和Sun PKCS11組態檔已正確設定，您可以使用以下命令（keytool已與Java JDK一起安裝）：

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

如果您在清單中看到您的憑證，表示HSM已正確設定。

>[!NOTE]
>
>從Java 1.7開始，適用於Windows的64位元Sun Java不支援Adobe存取DRM與HSM裝置通訊所需的PKCS11介面。 如果您打算使用HSM，請使用32位元版本的Java，或使用支援完整PKCS11介面的JDK。
