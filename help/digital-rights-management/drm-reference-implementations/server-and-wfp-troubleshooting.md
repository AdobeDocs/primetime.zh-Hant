---
title: 疑難排解
description: 疑難排解
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 疑難排解{#troubleshooting}

以下是部署過程中可能遇到的一些問題和解決方案。

* 如果顯示以下錯誤消息：

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   請確定密碼已使用`ScrambleUtil`類加密。

* 如果顯示以下錯誤消息：

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   請務必在PFX檔案中指定正確的加密密碼。

* 如果顯示以下錯誤消息：

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   請確定您使用Reference Implementation *隨附的密碼擾碼器類別*。 此擾碼器公用程式與Adobe PrimetimeDRM伺服器針對受保護串流提供的公用程式不同。

