---
title: 疑難排除
description: 疑難排除
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 疑難排除 {#troubleshooting}

以下列出部署的常見問題和解決方案：

* 如果看到以下錯誤：

  ```
      "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  請確定密碼已使用提供的加密 `ScrambleUtil` 類別。

* 如果看到以下錯誤：

  ```
      "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  請確定您為PFX檔案指定了正確的加密密碼。

* 如果看到以下錯誤：

  ```
      "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  請確定您使用了參考實作隨附的密碼Scrumbler類別(此Scrumbler公用程式與Adobe® Access™ Server for Protected Streaming隨附的公用程式不同)。
