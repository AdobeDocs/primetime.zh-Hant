---
description: SDK會定期下載Adobe所發佈的CRL。 您必須確保不會封鎖對這些檔案的存取，或不會阻止這些CRL的強制執行。
title: 使用Adobe發佈的CRL
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 使用Adobe發佈的CRL{#consuming-crls-published-by-adobe}

SDK會定期下載Adobe所發佈的CRL。 您必須確保不會封鎖對這些檔案的存取，或不會阻止這些CRL的強制執行。

SDK提供可在擷取AdobeCRL時忽略錯誤的設定選項，而且您只能在開發環境中套用此選項。 在生產環境中，授權伺服器必須從Adobe擷取CRL。 如果授權伺服器無法取得有效的CRL，則會發生錯誤。
