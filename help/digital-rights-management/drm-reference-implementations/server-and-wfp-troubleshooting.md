---
title: 故障排除
description: 故障排除
copied-description: true
exl-id: 6c4f15b6-507e-496e-ad1c-702ce77dd069
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 故障排除{#troubleshooting}

以下是在部署過程中可能遇到的一些問題和解決方案。

* 如果顯示以下錯誤消息：

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   確保密碼已使用 `ScrambleUtil` 類。

* 如果顯示以下錯誤消息：

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   確保在PFX檔案中指定了正確的加密密碼。

* 如果顯示以下錯誤消息：

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   確保使用密碼擾碼器類 *已提供的參考實施*。 此擾碼器實用程式與隨Adobe PrimetimeDRM伺服器提供的受保護流式管理實用程式不同。
