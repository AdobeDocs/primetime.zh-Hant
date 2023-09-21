---
title: 使用Adobe發佈的CRL
description: 使用Adobe發佈的CRL
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 使用Adobe發佈的CRL{#consume-crls-published-by-adobe}

SDK會定期下載Adobe發佈的CRL。 請勿封鎖對這些檔案的存取，或阻止強制實行這些CRL。

SDK提供可在擷取AdobeCRL時忽略錯誤的設定選項。 此選項只能用於開發環境。 在生產環境中，授權伺服器必須能夠從Adobe擷取CRL。 無法取得有效的CRL為錯誤。
