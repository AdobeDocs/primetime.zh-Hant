---
title: 疑難排解
description: 疑難排解
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# 疑難排解{#troubleshooting}

以下列出常見的部署問題和解決方案：

* 如果您看到下列錯誤：

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   請確定密碼是使用提供的`ScrambleUtil`類加密的。

* 如果您看到下列錯誤：

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   請務必為PFX檔案指定正確的加密密碼。

* 如果您看到下列錯誤：

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   請確定您使用了「參考實作」(Reference Implementation)中提供的密碼擾碼器類別(此擾碼器公用程式與「Adobe® Access™ Server for Protected Streaming」（受保護串流）中提供的不同)。

