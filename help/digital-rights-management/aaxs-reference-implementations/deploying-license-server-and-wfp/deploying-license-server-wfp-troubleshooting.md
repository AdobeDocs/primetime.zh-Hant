---
title: 故障排除
description: 故障排除
copied-description: true
exl-id: 4af7b625-63d3-48b6-98a5-b8894dd0c67f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 故障排除 {#troubleshooting}

下面列出了常見的部署問題和解決方案：

* 如果您看到以下錯誤：

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   確保使用提供的 `ScrambleUtil` 類。

* 如果您看到以下錯誤：

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   確保為PFX檔案指定了正確的加密密碼。

* 如果您看到以下錯誤：

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   確保您使用了「參考實現」提供的密碼加擾器類(此加擾器實用程式與「受保護流」Adobe® Access™伺服器提供的加擾器實用程式不同)。
