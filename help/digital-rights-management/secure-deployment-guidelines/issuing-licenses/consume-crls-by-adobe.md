---
description: SDK會定期下載由Adobe發佈的CRL。 您必須確保不會封鎖對這些檔案的存取，或不會妨礙這些CRL的執行。
title: 使用由Adobe發佈的CRL
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 使用Adobe{#consuming-crls-published-by-adobe}發佈的CRL

SDK會定期下載由Adobe發佈的CRL。 您必須確保不會封鎖對這些檔案的存取，或不會妨礙這些CRL的執行。

SDK有設定選項，可在擷取AdobeCRL時忽略錯誤，而您只能在開發環境中套用此選項。 在生產環境中，許可證伺服器必須從Adobe中檢索CRL。 如果授權伺服器無法取得有效的CRL，就會發生錯誤。
