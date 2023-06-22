---
title: 使用Adobe發佈的CRL
description: 使用Adobe發佈的CRL
copied-description: true
exl-id: b7f68a29-f834-4613-b64d-e610f660e6fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 使用Adobe發佈的CRL{#consume-crls-published-by-adobe}

SDK會定期下載Adobe發佈的CRL。 請勿封鎖對這些檔案的存取，或阻止這些CRL的強制執行。

SDK有設定選項，可在擷取AdobeCRL時忽略錯誤。 此選項只能用於開發環境。 在生產環境中，授權伺服器必須能夠從Adobe擷取CRL。 無法取得有效的CRL是錯誤。
