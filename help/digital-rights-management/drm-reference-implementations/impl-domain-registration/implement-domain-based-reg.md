---
title: 實施基於身份的域註冊
description: 實施基於身份的域註冊
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# 實施基於身份的域註冊{#implement-identity-based-domain-registration}

1. 建立具有強制域註冊的DRM策略。
1. 指定網域伺服器URL的伺服器主機和連接埠。

   在[!DNL .properties]檔案中，設定：

   ```
   policy.domain.url=https://[server:port] 
   ```

1. 使用使用者名稱和密碼進行驗證為強制性。

   在[!DNL .properties]檔案中，設定：

   ```
   policy.domain.anonymous=false 
   ```
