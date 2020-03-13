---
seo-title: 實施基於身份的域註冊
title: 實施基於身份的域註冊
uuid: 4a71b2e0-d1a2-4d63-9cbd-980a292774ab
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# 實施基於身份的域註冊{#implement-identity-based-domain-registration}

1. 建立具有強制域註冊的DRM策略。
1. 指定網域伺服器URL的伺服器主機和連接埠。

   在您的 [!DNL .properties] 檔案中，設定：

   ```
   policy.domain.url=https://[server:port] 
   ```

1. 使用使用者名稱和密碼進行驗證為強制性。

   在您的 [!DNL .properties] 檔案中，設定：

   ```
   policy.domain.anonymous=false 
   ```
