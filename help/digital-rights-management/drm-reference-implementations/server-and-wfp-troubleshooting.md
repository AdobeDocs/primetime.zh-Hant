---
title: 疑難排除
description: 疑難排除
copied-description: true
exl-id: 6c4f15b6-507e-496e-ad1c-702ce77dd069
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 疑難排除{#troubleshooting}

以下是您在部署期間可能會遇到的一些問題和解決方案。

* 如果顯示下列錯誤訊息：

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   確定密碼已使用 `ScrambleUtil` 類別。

* 如果顯示下列錯誤訊息：

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   請確定您已在PFX檔案中指定正確的加密密碼。

* 如果顯示下列錯誤訊息：

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   請確定您使用密碼加擾程式類別 *參考實作所提供的資源*. 此Scrambler公用程式與Adobe Primetime DRM Server for Protected Streaming隨附的公用程式不同。
