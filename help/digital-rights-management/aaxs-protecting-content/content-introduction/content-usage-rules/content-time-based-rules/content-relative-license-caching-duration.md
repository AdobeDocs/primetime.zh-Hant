---
title: 許可證快取持續時間
description: 許可證快取持續時間
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 許可證快取持續時間{#license-caching-duration}

指定許可證可以快取到客戶端本地許可證儲存中磁碟上而不需要從許可證伺服器重新獲取的持續時間。 您也可以指定一個絕對日期/時間，在此日期/時間之後，許可證將不能再快取。

一旦快取過期日期過後，許可證將不再有效，並且客戶端必須從許可證伺服器請求新的許可證。

示例用例：使用許可證快取持續時間來指定特定許可證的有效固定時間量，例如在租賃使用案例中。 可以指定30天租賃（使用許可證快取），以指示使用內容的總許可證持續時間。
