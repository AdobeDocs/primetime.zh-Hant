---
title: 實現基於身份的域註冊
description: 實現基於身份的域註冊
copied-description: true
exl-id: e2f826a8-eea5-4d5f-ac4d-401d7a6c5373
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# 實現基於身份的域註冊{#implement-identity-based-domain-registration}

1. 建立具有強制域註冊的DRM策略。
1. 指定域伺服器URL的伺服器主機和埠。

   在 [!DNL .properties] 檔案，設定：

   ```
   policy.domain.url=https://[server:port] 
   ```

1. 使用用戶名和密碼進行身份驗證成為必填項。

   在 [!DNL .properties] 檔案，設定：

   ```
   policy.domain.anonymous=false 
   ```
