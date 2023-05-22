---
title: 在BEES伺服器上配置SSL
description: 在BEES伺服器上配置SSL
copied-description: true
exl-id: 6823a71c-3be6-4c07-a3e6-e16bd931deaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 在BEES伺服器上配置SSL {#configure-ssl-on-your-bees-server}

1. 向提供此軟體的Adobe聯繫人提供伺服器SSL證書。

   該證書將作為受信任證書添加到Mighine Cloud DRM信任儲存。
1. 要為SSL連接啟用客戶端身份驗證（在此版本中禁用）:
   1. 添加 `[!DNL clouddrm-transport.cer]` 和 `[!DNL AdobeFlashAccessIntermediateCA.cer]` 用於客戶端身份驗證的信任儲存的證書。
   1. 在SSL配置中啟用客戶端身份驗證。
