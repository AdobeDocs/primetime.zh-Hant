---
title: 在您的BEES伺服器上設定SSL
description: 在您的BEES伺服器上設定SSL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# 在您的BEES伺服器上配置SSL {#configure-ssl-on-your-bees-server}

1. 將您的伺服器SSL憑證提供給提供此軟體的Adobe聯絡人。

   此憑證將新增為Primetime Cloud DRM信任商店的受信任憑證。
1. 要為SSL連接啟用客戶機驗證（在此版本中禁用）:
   1. 將`[!DNL clouddrm-transport.cer]`和`[!DNL AdobeFlashAccessIntermediateCA.cer]`憑證新增至用於用戶端驗證的信任存放區。
   1. 在SSL設定中啟用用戶端驗證。
