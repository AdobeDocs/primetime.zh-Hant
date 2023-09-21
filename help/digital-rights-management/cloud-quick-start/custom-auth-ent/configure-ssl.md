---
title: 在您的BEES伺服器上設定SSL
description: 在您的BEES伺服器上設定SSL
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 在您的BEES伺服器上設定SSL {#configure-ssl-on-your-bees-server}

1. 提供您的伺服器SSL憑證給提供此軟體的Adobe連絡人。

   此憑證將會新增為Primetime Cloud DRM信任存放區的信任憑證。
1. 啟用SSL連線的使用者端驗證（在此版本中停用）：
   1. 新增 `[!DNL clouddrm-transport.cer]` 和 `[!DNL AdobeFlashAccessIntermediateCA.cer]` 用於使用者端驗證之信任存放區的憑證。
   1. 在您的SSL設定中啟用使用者端驗證。
