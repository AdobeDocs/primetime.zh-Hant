---
title: 實作以身分為基礎的網域註冊
description: 實作以身分為基礎的網域註冊
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# 實作以身分為基礎的網域註冊{#implement-identity-based-domain-registration}

1. 建立具有強制網域註冊的DRM政策。
1. 指定網域伺服器URL的伺服器主機和連線埠。

   在您的 [!DNL .properties] 檔案，設定：

   ```
   policy.domain.url=https://[server:port] 
   ```

1. 強制使用使用者名稱和密碼進行驗證。

   在您的 [!DNL .properties] 檔案，設定：

   ```
   policy.domain.anonymous=false 
   ```
