---
seo-title: 在您的BEES伺服器上設定SSL
title: 在您的BEES伺服器上設定SSL
uuid: 041a106e-8b21-4018-815d-b7ea48c3de03
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 在您的BEES伺服器上設定SSL {#configure-ssl-on-your-bees-server}

1. 將您的伺服器SSL憑證提供給提供此軟體的Adobe聯絡人。

   此憑證將新增為Primetime Cloud DRM信任商店的受信任憑證。
1. 要為SSL連接啟用客戶機驗證（在此版本中禁用）:
   1. 將和證 `[!DNL clouddrm-transport.cer]` 書新 `[!DNL AdobeFlashAccessIntermediateCA.cer]` 增至用於用戶端驗證的信任存放區。
   1. 在SSL設定中啟用用戶端驗證。
