---
title: 使用由Adobe發佈的CRL
description: 使用由Adobe發佈的CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# 使用Adobe{#consume-crls-published-by-adobe}發佈的CRL

SDK會定期下載由Adobe發佈的CRL。 請勿阻止對這些檔案的訪問或阻止執行這些CRL。

SDK有設定選項，可在擷取AdobeCRL時忽略錯誤。 此選項只能用於開發環境。 在生產環境中，許可證伺服器必須能夠從Adobe中檢索CRL。 無法獲取有效的CRL是錯誤。
