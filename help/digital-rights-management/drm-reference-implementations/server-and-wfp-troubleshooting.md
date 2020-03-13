---
description: 'null'
seo-description: 'null'
seo-title: 疑難排解
title: 疑難排解
uuid: 06b86067-1ff6-4b4e-922f-7f968260ba19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 疑難排解{#troubleshooting}

以下是部署過程中可能遇到的一些問題和解決方案。

* 如果顯示以下錯誤消息：

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   請確定密碼已使用類加密 `ScrambleUtil` 。

* 如果顯示以下錯誤消息：

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   請務必在PFX檔案中指定正確的加密密碼。

* 如果顯示以下錯誤消息：

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   請確定您使用「參考實 *施」中提供的密碼擾碼器類別*。 此剪貼器公用程式與Adobe Primetime DRM Server針對受保護串流提供的公用程式不同。

