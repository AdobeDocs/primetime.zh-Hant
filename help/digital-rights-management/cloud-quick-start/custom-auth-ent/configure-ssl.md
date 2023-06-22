---
title: 在您的BEES伺服器上設定SSL
description: 在您的BEES伺服器上設定SSL
copied-description: true
exl-id: 6823a71c-3be6-4c07-a3e6-e16bd931deaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 在您的BEES伺服器上設定SSL {#configure-ssl-on-your-bees-server}

1. 將您的伺服器SSL憑證提供給提供此軟體的Adobe連絡人。

   此憑證將作為受信任的憑證新增到Primetime Cloud DRM信任存放區。
1. 啟用SSL連線的使用者端驗證（在此版本中停用）：
   1. 新增 `[!DNL clouddrm-transport.cer]` 和 `[!DNL AdobeFlashAccessIntermediateCA.cer]` 用於使用者端驗證之信任存放區的憑證。
   1. 在您的SSL設定中啟用使用者端驗證。
