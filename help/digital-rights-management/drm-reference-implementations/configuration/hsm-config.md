---
description: 可以使用支援HSM的Sun PKCS#11提供程式配置引用實現。 雖然不需要使用HSM，但建議使用。
title: HSM配置
exl-id: 87a7d242-8202-4749-91a6-e6697be6a61d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# HSM配置{#hsm-configuration}

可以使用支援HSM的Sun PKCS#11提供程式配置引用實現。 雖然不需要使用HSM，但建議使用。

要在HSM上使用憑據，必須為Sun PKCS#11提供程式建立配置檔案。 有關詳細資訊，請參見 [《 Java PCKS#11參考指南》](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html)。

要驗證是否配置了HSM和Sun PKCS#11配置檔案，請使用隨Java JDK安裝的keytool鍵入以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果可以在清單中查看憑據，則已正確配置了HSM。

>[!NOTE]
>
>從Java 1.7開始，64位Sun Java for Windows不再支援Adobe PrimetimeDRM與HSM設備通信所需的PKCS#11介面。 如果計畫使用HSM，請確保使用32位版本的Java或使用支援完整PKCS#11介面的JDK。
