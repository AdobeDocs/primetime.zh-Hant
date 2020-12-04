---
seo-title: 疑難排解
title: 疑難排解
uuid: db76d6a4-c285-4d86-95a1-4f1a85ed3743
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
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

   請確定您使用了「參考實作」(Reference Implementation)中提供的密碼scrambler類別（此crambler公用程式與Adobe® Access™ Server for Protected Streaming中提供的不同）。

