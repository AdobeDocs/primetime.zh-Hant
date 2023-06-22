---
title: 疑難排除
description: 疑難排除
copied-description: true
exl-id: 4af7b625-63d3-48b6-98a5-b8894dd0c67f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 疑難排除 {#troubleshooting}

以下列出部署的常見問題和解決方案：

* 如果您看到以下錯誤：

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   請確定密碼已使用提供的加密 `ScrambleUtil` 類別。

* 如果您看到以下錯誤：

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   請確定您為PFX檔案指定了正確的加密密碼。

* 如果您看到以下錯誤：

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   請確定您使用了參考實作隨附的Password Scrambler類別(此Scrambler公用程式不同於Adobe® Access™ Server for Protected Streaming)。
